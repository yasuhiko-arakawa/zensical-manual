---
icon: lucide/download
---

# インストール

uv を使って Zensical をインストールし、サイトを作成してプレビューするまでの手順です。

## 前提

- [uv](https://docs.astral.sh/uv/) がインストールされていること
- Python 3.13 以上(uv が自動で用意します)

## 1. プロジェクトを初期化する

作業用のフォルダを作成し、その中で実行します。

```powershell
uv init --bare --name zensical-manual
```

!!! warning "プロジェクト名を `zensical` にしない"

    プロジェクト名が `zensical` だと、uv は PyPI の Zensical ではなく
    プロジェクト自身を依存として扱います。`uv add zensical` が
    うまくいかず、`uv run zensical` を実行しても「Hello from zensical!」と
    表示されるだけになります。

    フォルダ名が `zensical` の場合は、上のように `--name` で別の名前
    (例: `zensical-manual`)を指定してください。`--bare` を付けると、
    `src/` やスクリプト定義が作られず、こうした衝突を避けられます。

## 2. Zensical を追加する

```powershell
uv add --dev zensical
```

インストールされたことは、バージョンの表示で確認できます。

```powershell
uv run zensical --version
```

## 3. サイトを作成する

```powershell
uv run zensical new .
```

次のファイルとフォルダが作成されます。

| 名前 | 内容 |
|---|---|
| `zensical.toml` | サイトの設定ファイル |
| `docs/` | サイトの原稿(Markdown) |
| `.github/workflows/docs.yml` | GitHub Pages へ公開するための設定 |

!!! info "最初に表示されるページ"

    作成直後は、`docs/index.md` にサンプルのトップページ(「Get started」)と、
    `docs/markdown.md` に Markdown の早見表が入っています。
    このマニュアルでは、それぞれ [初期ページ](default-index.md) と
    [Markdown in 5min](markdown.md) として残しています。

## 4. プレビューする

```powershell
uv run zensical serve
```

ブラウザで <http://localhost:8000> を開くと、サイトが表示されます。
ファイルを編集すると、表示は自動で更新されます。

## 5. ビルドする

公開用のファイルは、次のコマンドで `site/` に出力されます。

```powershell
uv run zensical build
```

!!! note

    uv のプロジェクトでは、コマンドを `uv run zensical ...` の形で実行します。
    仮想環境(`.venv\Scripts\activate`)を有効にした場合は、`uv run` を省略できます。

## 参考

- [Get started - Zensical](https://zensical.org/docs/get-started/)
- [Create your site - Zensical](https://zensical.org/docs/create-your-site/)
