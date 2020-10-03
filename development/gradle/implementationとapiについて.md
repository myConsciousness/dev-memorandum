# `implementation` と `api` について

## 概要

`Gradle` でビルド管理をしていて依存関係を記述する際に `implementation` や `api` というキーワードを使用するが、その概念と意味を理解できていなかったので学習した内容をまとめる。

詳細は後述するが、この両者の概念の違いは `依存関係の伝播可否` であった。

## `implementation` と `api` の違い

まず、`Gradle` で依存関係を記述する際には `implementation` や `api`　以外にも `compile`　や `runtime` が存在するが、現在では `implementation` と `api` キーワード以外は非推奨になっている。当時のトレンドの推移に関してはわからないが、`Gradle 3.4` で `Java Library Plugin` が追加されたことで先に挙げた `implementation` と `api` 以外のキーワードが公式に非推奨になったようだ。

> **_Note:_**</br>
> 公式に `deprecated` になったのはつい最近になってからのようで、`Gradle 4.7` における[Java Library](https://docs.gradle.org/4.7/userguide/java_plugin.html#sec:java_plugin_and_dependency_management)のドキュメントで明記された。

そのため、以下では非推奨になったキーワードに関しては割愛し、`implementation` キーワードと `api` キーワードの差異をまとめるに留める。

### 1. `implementation`

`implementation` キーワードを使用して記述された依存関係は **_伝播しない_** 。

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

`commons-lang3` に依存している `プロジェクトB` を使用している `プロジェクトA` にこの依存関係が伝播しないとは、つまり、**_`プロジェクトA` で `プロジェクトB` が依存している `commons-lang3` の機能を使用するためには別途 `プロジェクトA` で `commons-lang3` の依存関係を記述しなければならないということである。_**

### 2. `api`

`api` キーワードを使用して記述された依存関係は **_伝播する_** 。
また、`api` キーワードを使用する場合は `java-library` をプラグインに追加する必要がある。

例えば、`プロジェクトA` と `プロジェクトB` があると仮定して、以下のように依存関係が定義されているとする。

**_プロジェクト A_**

```groovy
dependencies {
    implementation プロジェクトB
}
```

**_プロジェクト B_**

```groovy
apply plugin: 'java-library'

dependencies {
    api 'org.apache.commons:commons-lang3:3.7'
}
```

上記の定義について補足すると、`commons-lang3` に依存している `プロジェクトB` に `プロジェクトA` が依存しているという図である。この場合の `プロジェクトB` で定義された依存関係は `プロジェクトA` に伝播する。

`commons-lang3` に依存している `プロジェクトB` を使用している `プロジェクトA` にこの依存関係が伝播するとは、つまり、**_`プロジェクトB` が依存している `commons-lang3` の依存関係を `プロジェクトA` の依存関係に追加しなくても `commons-lang3` の機能を使用することができるということである。_**

## `implementation` のメリット

公式ドキュメントでは、`compile` ではなく `implementation` を使うことについて、次のようなメリットがあると説明している。

1. コンパイル時に依存関係が利用側のどこにも漏れることがない。
   1. 従って、意図しない推移的な依存関係が発生することがない。
2. 取り除かれたクラスパスによってコンパイルがより早くなる。
3. `implementation` で指定した依存対象が変更されても、利用する側はリコンパイルの必要がない。
4. 新しい `Maven` プラグインと合わせて使うと、コンパイル時に必要になるライブラリと実行時に必要になるライブラリを明確に分けた `POM` ファイルを生成するようになり、綺麗な公開ができる。

**_要するに、`compile` を使用する方法には以下のような問題があった。_**

- 依存関係が全て推移的に伝播していくため、依存関係が不必要に拡大してしまっていた
- 内部 `API` のような外部に漏らしたくない依存関係まで広がっていた

これを `implementation` で定義することで、依存関係の不必要な拡大を防ぎ、本当に必要な依存関係だけを `api` で推移させられるようになる。また、`implementation` が依存関係を伝播させなくなることで、リコンパイルの頻度も減らせられるようになるメリットがある。

## `implementation` と `api` の使い分け

**_基本的には `implementation` を使用して依存関係を宣言すればよさそうである。_**

`api` キーワードを使用して依存関係を伝播させる場面がまだ掴めていないが、機能に依存している共通機能を使用するプロジェクトでも使用できるように伝播させるといった使い道があるのではないかと思う。

例えば、共通ライブラリ `common-something` に依存している `プロジェクトB` を使用する `プロジェクトA` でも依存関係を明示することなく `common-something` を使用したい場合は以下のような場合である。

**_プロジェクト A_**

```groovy
dependencies {
    implementation プロジェクトB
}
```

**_プロジェクト B_**

```groovy
apply plugin: 'java-library'

dependencies {
    api 'common-something'
}
```

上記のように依存関係を定義することで、使用者である `プロジェクトA` は共通機能の依存関係を意識しなくてもよくなる。
