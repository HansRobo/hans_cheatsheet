
---
title: docker
category: Tool
layout: 2017/sheet
tags: [Tools]
updated: 2024-11-03
created: 2024-11-03 13:17:00
weight: -10

## bashを使う

```docker
SHELL ["/bin/bash", "-c"]
```

参考：[Dockerfile リファレンス — Docker-docs-ja 24.0 ドキュメント](https://docs.docker.jp/engine/reference/builder.html#shell)

## ビルドのキャッシュは 3 種類

| 種類 | 何が残るか | CI へ運べるか |
|---|---|---|
| layer cache | 各命令の結果のレイヤー | `cache-to type=gha` / `type=registry` で運べる |
| mount cache（`RUN --mount=type=cache`） | パッケージマネージャ等の作業ディレクトリ | **運べない**（ビルダーのローカルだけ） |
| image store | ビルド済みイメージ | `docker pull` で運ぶ |

GitHub Actions で `cache-to: type=gha` を書いても、`--mount=type=cache` の中身は毎回空から始まる。apt / pip / cargo のキャッシュを CI で効かせたいなら、mount cache でなく layer に乗る形（依存のインストールを先の命令に分ける）にするか、ランナー側で永続化する。

参考: [The physics of Docker build caching（Blacksmith, 2026-07）](https://www.blacksmith.sh/blog/the-physics-of-docker-build-caching)（ランナー会社の記事。秒数の比較は同社計測）
