# Errors And Bugs

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

すべてのプログラマが異なるが、共通して経験することがある。それは、`エラーメッセージ` を受け取ることだ。
`エラー` や `バグ` は、プログラムが予期せぬ動作をする原因となります。

エラーメッセージが表示されたときは、ほとんどの場合、コードの中で何か間違って書いたことが原因です。
その結果、コンパイラはプログラムを翻訳できず、エラーメッセージを返します。

エラーにはさまざまな種類があります。
これは大変なことのように聞こえるかもしれませんが、幸いにも `Kotlinコンパイラ` は正確で説明的なエラーメッセージを提供してくれるので、問題を素早く効率的に見つけることができます。

例えば、以下のコードをよく見てみましょう。

```kotlin
fun main() {
  printlnn("To err is human.")
}
```

これを実行すると、以下のようなエラーが出ます。

```txt
Error.kt:2:3: error: unresolved reference: printlnn
  printlnn("To err is human.")
  ^
```

このエラーメッセージには、多くの有用な情報が記載されています。

- `Error.kt` はバグを含むファイルの名前です。
- 最初の数字 (2) は、エラーが存在する行を示します。
- 2 番目の数字 (3) は、エラーがその行に存在する文字番号を示します。
- error: の後に続くテキストは、どのようなエラーが発生したかを説明しています。

このエラーが発生したのは、println の代わりに printlnn を書いたためで、コンパイラはその命令を認識できませんでした。

コードを修正して再実行すると、以下のような出力が得られます。

```txt
To err is human.
```

## Instructions

### 1. Error.kt のコードを実行します

```txt
fun main() {
  println("An error a day keeps the programmer away."
}
```

**_出力:_**

```txt
Error.kt:2:54: error: expecting ')'
  println("An error a day keeps the programmer away."
                                                     ^
```

### 2. エラーメッセージを読み、エディタでコードを修正して正常に実行できるようにしてください

```kotlin
fun main() {
  println("An error a day keeps the programmer away.")
}
```

**_出力:_**

```txt
An error a day keeps the programmer away.
```
