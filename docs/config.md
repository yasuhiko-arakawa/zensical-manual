---
icon: lucide/settings
---

# 設定ファイル

サイトの設定は、プロジェクト直下の `zensical.toml` に書きます。
このページでは、このマニュアルで実際に使っている項目を中心に説明します。
すべての項目は、[公式の設定リファレンス](https://zensical.org/docs/setup/basics/)で確認できます。

## 基本の設定

サイト全体の設定は、`[project]` の下に書きます。

```toml
[project]
site_url = "https://<ユーザー名>.github.io/<リポジトリ名>/"
site_name = "Zensical マニュアル"
copyright = "Copyright &copy; 2026 Yasuhiko Arakawa"
```

| 項目 | 内容 |
|---|---|
| `site_name` | サイト名。ページのヘッダーなどに表示される(必須) |
| `site_url` | 公開先の URL。GitHub Pages では `https://<ユーザー名>.github.io/<リポジトリ名>/` の形で、末尾に `/` を付ける |
| `site_description` | サイトの説明。ページに個別の説明がないときに使われる |
| `site_author` | サイトの作成者 |
| `copyright` | フッターの著作権表示。HTML の断片も書ける(`&copy;` など) |

### そのほかの項目

次の項目は、`zensical new` が作成した `zensical.toml` には書かれていません。
変更したいときに、`[project]` の下に追記します。

```toml
[project]
site_name = "Zensical マニュアル"
docs_dir = "docs"
```

!!! warning "`[project]` は 1 回だけ書く"

    `[project]` を 2 回書くと、TOML のエラーになります。既存の `[project]` の中に、1 行足してください。
    また、`[project.theme]` などの見出しより後に書くと、その見出しの項目として扱われます。
    `[project]` の項目は、ほかの見出しより前に置いてください。

| 項目 | 内容 | 既定値 |
|---|---|---|
| `docs_dir` | 原稿(Markdown)を置くフォルダ | `docs` |
| `site_dir` | ビルドの出力先 | `site` |
| `use_directory_urls` | `false` にすると、URL が `/file/` ではなく `/file.html` の形になる | `true` |
| `dev_addr` | `serve` で使うアドレスとポート | `localhost:8000` |

## ナビゲーション

`nav` で、サイドバーのページ構成を決めます。
`{ "表示名" = "ファイル名" }` の形で並べ、リストを入れ子にすると階層になります。

```toml
nav = [
  { "ホーム" = "index.md" },
  { "インストール" = "install.md" },
  { "デフォルトのページ" = [
    { "初期ページ" = "default-index.md" },
    { "Markdown in 5min" = "markdown.md" },
  ] },
]
```

!!! note

    `nav` に書かなかったページも、ビルドの出力には含まれます。
    URL を直接開けば見られますが、ナビゲーションには表示されません。

## 配色 { #palette }

ライトとダークの切り替えは、`palette` で設定します。
このマニュアルでは、2つの配色を切り替える設定にしています。

```toml
[[project.theme.palette]]
scheme = "default"
toggle.icon = "lucide/sun"
toggle.name = "Switch to dark mode"

[[project.theme.palette]]
scheme = "slate"
toggle.icon = "lucide/moon"
toggle.name = "Switch to light mode"
```

- `scheme = "default"` がライト、`scheme = "slate"` がダークです。
- 最初に表示されるのは、1つ目に書いた配色です。
- OS の設定に合わせて自動で切り替えたい場合は、それぞれに
  `media = "(prefers-color-scheme: light)"` と `media = "(prefers-color-scheme: dark)"` を追加します。
- 色の指定(`primary`、`accent`)などは、[公式の配色の説明](https://zensical.org/docs/setup/colors/)を参照してください。

## 書く場所の一覧

| 項目 | 書く場所 |
|---|---|
| `site_name`、`site_url`、`copyright`、`nav`、`docs_dir` など | `[project]` |
| `language` | `[project.theme]` |
| `palette`(ライトとダークの切り替え) | `[[project.theme.palette]]`(2 つ並べる) |

## 設定を変えたら

`uv run zensical serve` でプレビュー中に、`docs/` の Markdown を編集した場合は、自動で反映されます。
`zensical.toml` を編集した場合の挙動は公式に記載がないため、反映されないときは、サーバーを再起動してください。

## 参考

- [Basics - Zensical](https://zensical.org/docs/setup/basics/)
- [Colors - Zensical](https://zensical.org/docs/setup/colors/)
