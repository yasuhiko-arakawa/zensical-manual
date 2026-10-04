---
icon: lucide/refresh-cw
---

# 更新と引き継ぎ

公開したマニュアルを更新する手順と、別のパソコンで作業を始める手順をまとめます。

## 日常の更新

1. **プレビューを起動する。**

    ```powershell
    uv run zensical serve --open
    ```

2. **`docs/` の Markdown を編集する。** 保存すると、ブラウザの表示が自動で更新されます。
3. **公開前にビルドを確認する。** エラーが出ないことを確認します。

    ```powershell
    uv run zensical build --clean
    ```

4. **commit して push する。**

    ```powershell
    git add .
    git commit -m "更新内容の説明"
    git push
    ```

5. **公開を確認する。** GitHub の **Actions** タブで「Documentation」が成功(緑)になれば、サイトが更新されています。

### ページを追加するとき

1. `docs/` に、新しい Markdown ファイルを作ります(例: `docs/usage.md`)。
2. `zensical.toml` の `nav` に、表示名とファイル名を書き足します。

    ```toml
    nav = [
      { "ホーム" = "index.md" },
      { "使い方" = "usage.md" },
    ]
    ```

3. 上の手順で、プレビューと push を行います。

!!! note

    `nav` に書かないページも出力には含まれますが、ナビゲーションには表示されません。
    詳しくは、[設定ファイル](config.md)を参照してください。

## 別のパソコンで始める

リポジトリを取得し、環境を再現します。

### 必要なもの

- [uv](https://docs.astral.sh/uv/)
- Git
- VS Code などのエディタ

### 手順

1. **リポジトリを clone する。**

    ```powershell
    git clone https://github.com/<ユーザー名>/<リポジトリ名>.git
    cd <リポジトリ名>
    ```

2. **環境を作る。** `pyproject.toml` と `uv.lock` にもとづいて、Python と Zensical が入ります。

    ```powershell
    uv sync
    ```

3. **プレビューで確認する。**

    ```powershell
    uv run zensical serve --open
    ```

### 最初に確認すること

- **Git の作成者情報。** パソコンごとに設定が必要です。意図しないアカウントの名前やメールアドレスが、コミットに残らないようにします。

    ```powershell
    git config user.name
    git config user.email
    ```

- **GitHub の認証。** push のときに、使いたいアカウントでログインしていることを確認します。

`.venv/`、`site/`、`.cache/` は Git に含めていません。clone した直後には存在せず、`uv sync` や `serve` で作られます。
