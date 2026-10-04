---
icon: lucide/pencil-line
---

# ページの書き方

ページの先頭に書く設定(フロントマター)と、このマニュアルで使っている拡張記法をまとめます。
Markdown の基本は [Markdown in 5min](markdown.md)、図・数式・脚注などの例は[初期ページ](default-index.md)を参照してください。

## フロントマター

ページの先頭を `---` で囲むと、そのページだけの設定を書けます。

```markdown
---
icon: lucide/book-open
title: ナビゲーションに出るタイトル
description: ページの説明
---

# ページの見出し
```

| 項目 | 内容 |
|---|---|
| `icon` | ナビゲーションに表示するアイコン |
| `title` | ナビゲーションとブラウザのタブに出るタイトルを、見出しとは別に指定する |
| `description` | 検索エンジン向けのページの説明(HTML の `meta` タグに入る) |
| `hide` | 目次やナビゲーションなどを隠す(`navigation`、`toc`、`path`、`footer` など) |
| `status` | ナビゲーションに状態(`new` など)を表示する。事前に設定ファイルで定義が必要 |

`hide` は、複数ある場合にリストで書きます。

```yaml
hide:
  - navigation
  - toc
```

### ページアイコン

`icon` には、`アイコンセット名/アイコン名` の形で書きます。

```yaml
icon: lucide/rocket
icon: simple/markdown
```

Zensical には、次の 5 種類のアイコンセットが入っています。

| セット | 特徴 |
|---|---|
| Lucide(`lucide/`) | 統一感のあるシンプルなアイコン。このマニュアルで使用 |
| Simple Icons(`simple/`) | ブランドやロゴ |
| Material Design Icons | Google のマテリアルデザイン |
| FontAwesome | 定番の Web アイコン(無料分) |
| Octicons | GitHub のアイコン |

アイコン名は、各セットの公式サイト(Lucide なら [lucide.dev](https://lucide.dev/))で検索できます。

### 文中でアイコンを使う

文章の中では、アイコン名の `/` を `-` に変えて、`:` で囲みます。

```markdown
:lucide-heart: が好き
```

表示例:

:lucide-heart: が好き

ページアイコンは、このページの左側のナビゲーションで確認できます。

## 注意書き

`!!!` に種類を続け、内容は 4 文字分字下げします。

```markdown
!!! note

    補足の内容です。
```

表示例:

!!! note

    補足の内容です。

使える種類は、`note`、`abstract`、`info`、`tip`、`success`、`question`、`warning`、`failure`、`danger`、`bug`、`example`、`quote` の 12 個です。
このマニュアルでは、補足に `note`、注意に `warning`、補足情報に `info` を使っています。

タイトルを変えるときは、種類の後ろに文字列を書きます。

```markdown
!!! warning "公開範囲に注意"

    内容です。
```

表示例:

!!! warning "公開範囲に注意"

    内容です。

`!!!` を `???` に変えると、クリックで開く折りたたみになります。`???+` なら、最初から開いた状態です。

```markdown
??? info "詳しい説明"

    クリックすると開きます。
```

表示例:

??? info "詳しい説明"

    クリックすると開きます。

## コードブロック

3 つのバッククォートの後ろに、言語名を書きます。

````markdown
```powershell
uv run zensical serve
```
````

表示例:

```powershell
uv run zensical serve
```

| 機能 | 書き方 |
|---|---|
| ファイル名の表示 | ` ```toml title="zensical.toml" ` |
| 行番号 | ` ```toml linenums="1" ` |
| 行の強調 | ` ```toml hl_lines="2 3" ` |

これらは組み合わせられます。

````markdown
```toml title="zensical.toml" linenums="1" hl_lines="2 3"
[project]
site_name = "Zensical マニュアル"
site_url = "https://example.com/"
```
````

表示例:

```toml title="zensical.toml" linenums="1" hl_lines="2 3"
[project]
site_name = "Zensical マニュアル"
site_url = "https://example.com/"
```

コピーボタンは、このマニュアルでは設定ファイルで全体に有効にしてあります(`content.code.copy`)。右上のボタンから、内容をコピーできます。

## タブ

内容を切り替えて見せたいときは、`===` を使います。内容は 4 文字分字下げします。

````markdown
=== "PowerShell"

    ```powershell
    uv run zensical serve
    ```

=== "Bash"

    ```bash
    uv run zensical serve
    ```
````

表示例:

=== "PowerShell"

    ```powershell
    uv run zensical serve
    ```

=== "Bash"

    ```bash
    uv run zensical serve
    ```

!!! note

    これらの記法は、`zensical.toml` の `[project.markdown_extensions]` で有効にしています。
    `zensical new` で作成した状態では、すべて有効です。

## 参考

- [Front matter - Zensical](https://zensical.org/docs/authoring/frontmatter/)
- [Icons, Emojis - Zensical](https://zensical.org/docs/authoring/icons-emojis/)
- [Admonitions - Zensical](https://zensical.org/docs/authoring/admonitions/)
- [Code blocks - Zensical](https://zensical.org/docs/authoring/code-blocks/)
- [Content tabs - Zensical](https://zensical.org/docs/authoring/content-tabs/)
