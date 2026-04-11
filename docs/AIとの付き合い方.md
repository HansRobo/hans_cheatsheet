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

