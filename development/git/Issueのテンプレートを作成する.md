# Issue のテンプレートを作成する方法

## やりたいこと

`Github` での `Issue` を機能追加やバグ報告などの用途に合わせてテンプレート化したい。

## 方法

### 1. `master` ブランチにテンプレート格納用のフォルダを作成

- 作成するフォルダ
  - `.github`
    - `ISSUE_TEMPLATE`

> Note:<br>
> 作成したテンプレートは `Github` の機能が参照するためファイル名は上記の通りにする必要がある

**_参考ツリー_**

```cmd
root
└─.github
   └─ISSUE_TEMPLATE
```

### 2. `ISSUE_TEMPLATE` フォルダにテンプレートを作成

先に作成した `ISSUE_TEMPLATE` にマークダウン方式のテンプレートを作成する。
拡張子は `.md` とする。

**_バグ報告用のテンプレート例_**

```yaml
---
name: Bug Report
about: Report a bug to improve functionality
labels: "bug"
assignees: "myConsciousness"
---
# Bug Report

## 1. Bug Details

## 2. What you did caused that bug

## 3. How it should be

## 4. References
```

`YAML frontmatter` を追加することで `Issue` の初期設定を定義することができる。

> Note:<br>
> この `YAML frontmatter` は別名で `metadata block` と呼ばれており、文章自体には含まれない、著者、キーワード、タイトルなどの情報を記述するための、メタ変数の並びを表現するための記述。3 つのハイフン(---)を書いた行で始まり、3 つのハイフンまたはピリオドを書いた行で終わる

```yaml
---
name: Bug Report
about: Report a bug to improve functionality
labels: "bug"
assignees: "myConsciousness"
---

```

### 3. `ISSUE_TEMPLATE` フォルダに作成したテンプレートをコミット

`ISSUE_TEMPLATE` フォルダに作成したテンプレートをコミットし、`Github` から`Issue` を新規作成しようとすると先にコミットしたテンプレートの選択画面に遷移する。

使用したいテンプレートを選択したらいつものように `Issue` を記述し発行する。

## 参考

- [リポジトリ用の単一 Issue テンプレートを手動で作成する](https://docs.github.com/ja/github/building-a-strong-community/manually-creating-a-single-issue-template-for-your-repository)
