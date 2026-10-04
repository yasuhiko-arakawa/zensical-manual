# Zensical マニュアル

Zensical でドキュメントサイトを作成し、GitHub Pages で公開するまでの手順をまとめたマニュアルです。

公開先: https://yasuhiko-arakawa.github.io/zensical-manual/

## ローカルで確認する

[uv](https://docs.astral.sh/uv/) が必要です。

```powershell
uv sync
uv run zensical serve --open
```

## 公開

`master` または `main` ブランチに push すると、GitHub Actions が自動でビルドして GitHub Pages に公開します。

## 構成

- `docs/`: 原稿(Markdown)
- `zensical.toml`: サイトの設定
- `.github/workflows/docs.yml`: 公開用のワークフロー
