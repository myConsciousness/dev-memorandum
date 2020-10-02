b# implementation と api について

## 概要

`Gradle` でビルド管理をしていて依存関係を記述する際に `implementation` や `api` というキーワードを使用するが、その概念と意味を理解できていなかったので学習した内容をまとめる。

詳細は後述するが、この両者の概念の違いは `依存関係の伝播可否` であった。

## implementation と api キーワードの違い

まず、`Gradle` で依存関係を記述する際には `implementation` や `api`　以外にも `compile`　や `runtime` が存在するが、現在では `implementation` と `api` キーワード以外は非推奨になっている。当時のトレンドの推移に関してはわからないが、`Gradle 3.4` で `Java Library Plugin` が追加されたことで先に挙げた `implementation` と `api` 以外のキーワードが公式に非推奨になったようだ。

> **_Note:_**</br>
> 公式に `deprecated` になったのはつい最近になってからのようで、`Gradle 4.7` における[Java Library](https://docs.gradle.org/4.7/userguide/java_plugin.html#sec:java_plugin_and_dependency_management)のドキュメントで明記された。

そのため、以下では非推奨になったキーワードに関しては割愛し、`implementation` キーワードと `api` キーワードの差異をまとめるに留める。

### 1. implementation

### 2. api
