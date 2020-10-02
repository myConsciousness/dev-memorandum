# implementation と api について

## 概要

`Gradle` でビルド管理をしていて依存関係を記述する際に `implementation` や `api` というキーワードを使用するが、その概念と意味を理解できていなかったので学習した内容をまとめる。

詳細は後述するが、この両者の概念の違いは `依存関係の伝播可否` であった。

## implementation と api キーワードの違い

まず、`Gradle` で依存関係を記述する際には `implementation` や `api`　以外にも `compile`　や `runtime` が存在するが、現在では `implementation` と `api` キーワード以外は非推奨になっている。当時のトレンドの推移に関してはわからないが、`Gradle 3.4` で `Java Library Plugin` が追加されたことで先に挙げた `implementation` と `api` 以外のキーワードが公式に非推奨になったようだ。

> **_Note:_**</br>
> 公式に `deprecated` になったのはつい最近になってからのようで、`Gradle 4.7` における[Java Library](https://docs.gradle.org/4.7/userguide/java_plugin.html#sec:java_plugin_and_dependency_management)のドキュメントで明記された。

そのため、以下では非推奨になったキーワードに関しては割愛し、`implementation` キーワードと `api` キーワードの差異をまとめるに留める。

### 1. implementation

`implementation` キーワードを使用して記述された依存関係は**_伝播しない_**。

例えば、`プロジェクトA` と `プロジェクトB` があると仮定して、以下のように依存関係が定義されているとする。

**_プロジェクト A_**

```groovy
dependencies {
    implementation プロジェクトB
}
```

**_プロジェクト B_**

```groovy
dependencies {
    implementation 'org.apache.commons:commons-lang3:3.7'
}
```

上記の定義について補足すると、`commons-lang3` に依存している `プロジェクトB` に `プロジェクトA` が依存しているという図である。この場合の `プロジェクトB` で定義された依存関係は `プロジェクトA` に伝播しない。

`commons-lang3` に依存している `プロジェクトB` を使用している `プロジェクトA` にこの依存関係が伝播しないとは、つまり、**_`プロジェクトA` で `プロジェクトB` が依存している `commons-lang3` の機能を使用するためには別途 `プロジェクトA` で `commons-lang3` の依存関係を記述しなければならない。_**

### 2. api
