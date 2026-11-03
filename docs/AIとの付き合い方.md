---
created: 2025-01-14 04:48:47
---

## 完璧を求めない

人間なら間違えても許されるようなタスクでも、AIが相手になった途端完璧を求めて「使えない」という人も多い。
完璧かそうじゃないか、という解像度の低い使い方はせずに、人間相手にそうやっているように、性能に応じた期待値を自分の中で適切に設定して使う。

## 得意なことを把握して使う

## Claude Code 複数アカウントの使い分け

Claude Code は `CLAUDE_CONFIG_DIR` 環境変数で設定ディレクトリを切り替えることで、複数のアカウントやプロファイルを使い分けられる。

### 仕組み

| 環境変数 | 役割 |
|---|---|
| `CLAUDE_CONFIG_DIR` | 設定・認証情報の保存先ディレクトリを変更する。デフォルトは `~/.claude` |
| `ANTHROPIC_AUTH_TOKEN` | Anthropic以外のプロバイダーや別アカウントのAPIキーを上書き指定する |

### 設定ディレクトリの構造

`CLAUDE_CONFIG_DIR` が指すディレクトリの中は以下のような構成になっている。

```
~/.claude/                   ← デフォルト（CLAUDE_CONFIG_DIR 未指定時）
~/.claude/profiles/xxx/      ← プロファイルごとのディレクトリ
├── CLAUDE.md                # そのプロファイル用のグローバル指示
├── settings.json            # モデル・権限などの設定
├── history.jsonl            # 会話履歴インデックス
├── sessions/                # 会話セッションの実データ
├── projects/                # プロジェクトごとのメモリ
├── hooks/                   # イベントフック定義
├── commands/                # カスタムスラッシュコマンド
└── ...
```

プロファイルを切り替えると、**認証情報・会話履歴・メモリ・CLAUDE.md・設定がすべて独立する**。
逆に言うと、プロファイルを作るだけでは `~/.claude` の内容は引き継がれないため、必要な設定は各プロファイルにコピーするか、シンボリックリンクで共有する。

### bashrc での実装例

```bash
# ~/.bashrc
claude-profileA() { claude "$@"; }  # デフォルト設定をそのまま使う
claude-profileB() { CLAUDE_CONFIG_DIR=~/.claude/profiles/profileB claude "$@"; }
claude-profileC() { CLAUDE_CONFIG_DIR=~/.claude/profiles/profileC ANTHROPIC_AUTH_TOKEN="$SOME_API_KEY" claude "$@"; }
```

各関数は `"$@"` でそのまま引数を渡すため、通常の `claude` コマンドと同じオプションが使える（例: `claude-profileB --resume`）。

### 使い分けの目的

- **設定ディレクトリの分離**: CLAUDE.md やメモリ・会話履歴をプロファイルごとに独立させられる
- **複数アカウント**: 個人・仕事など用途の異なるアカウントをターミナル上で素早く切り替えられる
- **別プロバイダー対応**: `ANTHROPIC_AUTH_TOKEN` を上書きすることで独自APIキーが必要なプロバイダーも利用できる


## Claude Code の小技と罠（2026-11 時点）

- **サブエージェントの要約生成を止める**: 2.1.232 からサブエージェントのステータス用に `agent_summary` が既定で生成され、利用枠を食う。`BUN_OPTIONS="--preload=<path>/no-agent-summary.js" claude` で止められる（アップデートで外れることがある。`CLAUDE_CODE_FORK_SUBAGENT=0` で止まるかは issue で意見が割れている）。参考: [gist: no-agent-summary](https://gist.github.com/flamerix-ai/c3905705cc4205e5de3011fa2e74efce)
- **作業フォルダの外への書込を止める**: 2.1.314 で `permissions.blockWritesOutsideWorkingDirectories` が入った。Write/Edit/NotebookEdit が対象で、**Bash は対象外**
- **hook が落ちると操作が通る**: hook の起動失敗や時間切れは既定で「通す」。止めたい hook には `onFailure: "block"` を付ける
- **同じセッションでモデルを変えない**: モデルを切り替えるとプロンプトキャッシュを作り直す（2 万トークン超の再書込。Windows Git Bash での測定）
- 2.1.317: ディスク満杯で `-p` が exit 0 になる不具合の修正、Ctrl+C で裏のエージェントが全停止。2.1.316: 11/30 に Opus 4.8 の fast mode を削除

## Grok Build CLI を X 検索だけに使う

X 検索を持つのは Grok だけ。検索結果を素早く得るだけなら、サブエージェントとターン数を絞る。

```bash
grok --no-subagents --max-turns 6 -p "x_search で <語> を Latest で探して URL と要点を列挙"
```

割引で 2027 年 5 月まで月 960 円（2026-11 の投稿）。headless で本格的に回すときの形は [[X探索 第5弾 テーマ台帳（中身を豊かにする）— 2026-11]] の `run.sh`（Write/Edit/Bash を deny、`--max-turns 60`）。

## 起動ディレクトリの罠（Codex / Claude Code）

Downloads のような「他人のファイルが落ちてくる場所」でエージェントを起動しない。そこに置かれた `AGENTS.md` / `CLAUDE.md` が読まれ、`~/.codex/config.toml` の `[mcp_servers.*]` を書き換える手口が報告されている（セキュリティ会社の記事で、自社製品の紹介を兼ねる）。参考: [Hijacking AI agents via the Downloads folder](https://forever.security/blog/hijacking-ai-agents-via-downloads-folder)
