---
icon: lucide/image
---

# 画像とリンク

ページ間のリンクと、画像の書き方をまとめます。

## ページ間のリンク

別のページへのリンクは、**HTML ではなく、Markdown ファイルへの相対パス**で書きます。
Zensical が、ビルド時に正しい HTML のリンクへ変換します。

```markdown
[インストール](install.md)
[設定ファイル](config.md)
```

表示例:

[インストール](install.md)  
[設定ファイル](config.md)

フォルダが違うページへは、`..` で上の階層をたどります。

```markdown
[Markdown の書き方](../default/markdown.md)
```

!!! note

    このマニュアルの `docs/` には、フォルダを分けたページがないため、上の例は表示していません。

### 見出しへのリンク

ファイル名の後ろに `#` と見出しのアンカーを付けます。

```markdown
[配色の設定](config.md#palette)
```

表示例:

[配色の設定](config.md#palette)

英語の見出しのアンカーは、小文字とハイフンの形(`## Color palette` なら `#color-palette`)になります。
一方、**日本語の見出しは `#_2`、`#_3` のような連番になり**、見出しの文字は使われません。
連番は、見出しを追加するとずれてしまいます。

リンクされる見出しには、アンカーを自分で付けておくと安全です。見出しの後ろに `{ #名前 }` を書きます。

```markdown
## 配色 { #palette }
```

!!! note

    この書き方は、`attr_list` という Markdown 拡張で動きます。
    このマニュアルの[設定ファイル](config.md#palette)の「配色」の見出しが、実際の例です。

### 外部サイトへのリンク

通常の Markdown と同じです。

```markdown
[Zensical 公式サイト](https://zensical.org/)
```

表示例:

[Zensical 公式サイト](https://zensical.org/)

!!! warning "絶対パスのリンクは避ける"

    `/docs/install/` のような絶対パスは、手元のプレビューでは動いても、
    公開後に壊れることがあります。相対パスで書けば、`site_url` を変えても
    リンクを直さずに済みます。

## 画像

画像は、`docs/` の中に置きます。リンクと同じく、書いているページからの相対パスで指定します。

```markdown
![説明文](image.png)
![説明文](images/screen.png)
![説明文](../assets/screen.png)
```

- 1 つ目は、同じフォルダにある画像です。
- 2 つ目は、`images/` フォルダの中の画像です。
- 3 つ目は、1 つ上の階層の `assets/` にある画像です。

`![ ]` の中の説明文は、画像が表示されないときや、読み上げで使われます。内容が分かる文を書いてください。

以降の表示例では、このマニュアルの `docs/images/` に置いたサンプル画像を使います。

```markdown
![サンプル画像](images/sample.svg)
```

表示例:

![サンプル画像](images/sample.svg)

### 大きさと位置

`{ }` の中に属性を書きます。

```markdown
![サンプル画像](images/sample.svg){ width="150" }
```

表示例(幅 150):

![サンプル画像](images/sample.svg){ width="150" }

`align=left` または `align=right` を付けると、文章が画像の横に回り込みます。
画面が狭いときは、画像は幅いっぱいに表示されます。

```markdown
![サンプル画像](images/sample.svg){ align=right width="150" }
```

表示例:

![サンプル画像](images/sample.svg){ align=right width="150" }

画像の左側に文章が回り込みます。画面幅が広いと、この文章が画像の横に並びます。
文章が何行か続くと、回り込みの様子が分かりやすくなります。
この段落は、回り込みを確認するための文章です。
画面が狭いときは、画像が幅いっぱいに表示され、文章は画像の下に移ります。

<div style="clear: both"></div>

### キャプション

図の説明を付けたいときは、`<figure>` を使います。

```markdown
<figure markdown="span">
![サンプル画像](images/sample.svg){ width="300" }
<figcaption>図 1: サンプル画像</figcaption>
</figure>
```

表示例:

<figure markdown="span">
![サンプル画像](images/sample.svg){ width="300" }
<figcaption>図 1: サンプル画像</figcaption>
</figure>

### ライトモードとダークモードで画像を切り替える

画像の名前の後ろに、`#only-light` または `#only-dark` を付けます。

```markdown
![ライト用](images/sample-light.svg#only-light)
![ダーク用](images/sample-dark.svg#only-dark)
```

表示例(右上のボタンで、ライトとダークを切り替えてみてください):

![ライト用](images/sample-light.svg#only-light)
![ダーク用](images/sample-dark.svg#only-dark)

### 読み込みを遅らせる

画像が多いページでは、`loading=lazy` を付けると、画面に近づくまで読み込まれません。

```markdown
![サンプル画像](images/sample.svg){ loading=lazy }
```

見た目は変わらないため、表示例は省略します。

!!! note

    `{ }` の属性は、`attr_list` という Markdown 拡張で動きます。
    `<figure>` の中に Markdown を書く記法は `md_in_html` です。
    このマニュアルの `zensical.toml` では、どちらも有効になっています。

## 参考

- [Links - Zensical](https://zensical.org/docs/authoring/markdown/)
- [Images - Zensical](https://zensical.org/docs/authoring/images/)
