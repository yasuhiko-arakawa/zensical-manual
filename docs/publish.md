---
icon: lucide/globe
---

# GitHub への公開

作成したサイトを GitHub Pages で公開する手順です。
`zensical new` が作成した `.github/workflows/docs.yml` により、
push するたびにビルドと公開が自動で行われます。

## 1. site_url を設定する

`zensical.toml` の `site_url` を、公開先の URL に書き換えます。

```toml
[project]
site_url = "https://<ユーザー名>.github.io/<リポジトリ名>/"
site_name = "サイト名"
```

!!! note

    末尾の `/` を付けてください。ユーザー名やリポジトリ名が違うと、
    公開後にスタイルが崩れたり、リンクが切れたりします。

## 2. リポジトリを作成する

GitHub で空のリポジトリを作成します。README などは追加しません。

## 3. 作成者情報を確認する

コミットに残る名前とメールアドレスを、push の前に確認します。
意図しないアカウントの情報が履歴に残らないようにするためです。

```powershell
git config user.name
git config user.email
```

このリポジトリだけ変えたい場合は、次のように設定します。

```powershell
git config user.name "<名前>"
git config user.email "<メールアドレス>"
```

## 4. .gitignore を用意する

ビルドの出力や仮想環境は、Git に含めません。

```gitignore
# Zensical build output and cache
site/
.cache/

# Python / uv
.venv/
__pycache__/
*.py[cod]
```

`uv.lock` は、環境を再現するために Git に含めます。

## 5. push する

```powershell
git add .
git commit -m "Initial manual site"
git remote add origin https://github.com/<ユーザー名>/<リポジトリ名>.git
git push -u origin <ブランチ名>
```

ワークフローは `main` と `master` の両方で動きます。
ブランチ名は `git branch --show-current` で確認できます。

!!! info "改行コードの警告"

    `git add` で「LF will be replaced by CRLF」という警告が出ることがあります。
    Windows の Git が改行コードを変換するという予告で、エラーではありません。
    動作に影響はないので、そのまま進めて構いません。

## 6. GitHub Pages を有効にする

初回のみ設定します。

1. リポジトリの **Settings** → **Pages** を開きます。
2. **Build and deployment** の **Source** を **GitHub Actions** にします。

## 7. 公開を確認する

1. **Actions** タブで、「Documentation」の実行が成功(緑)になるまで待ちます。
2. `site_url` に設定した URL を開いて、表示を確認します。

## うまくいかないとき

| 症状 | 対処 |
|---|---|
| `src refspec main does not match any` | ローカルのブランチ名が違います。`git branch` で確認し、そのブランチ名で push します。 |
| Pages の設定前に push して Actions が失敗した | Actions タブで該当の実行を開き、**Re-run all jobs** で再実行します。 |
| 別のアカウントで push される | リモート URL と、Windows の資格情報マネージャーに保存された認証情報を確認します。 |
| 画面が崩れる、リンクが切れる | `site_url` のユーザー名とリポジトリ名を確認します。 |

!!! warning "公開範囲に注意"

    GitHub Pages のサイトは、リポジトリが private でも、プランによっては
    インターネットに公開されます。社内向けの内容は、公開範囲を確認してから
    push してください。
