# Review

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

お疲れさまです。

これで、データ型と変数のセクションの最初のレッスンが完了しました。
ここで取り上げた内容を復習してみましょう。

- 変数の宣言は、val または var キーワードの後に名前、コロン、データ型が続きます。
- 変数の初期化は、代入演算子(=)を使用して変数に値が代入されたときに発生します。
- 変数の宣言と初期化は、1 行で同時に行うことも、別々に行うこともできます。
- 可変な変数は、var キーワードで表され、プログラム全体で変化すると予想される値を表します。
- 不変な変数は val キーワードで表され、一定の値を表します。
- Kotlin は型推論によって変数の型を推測することができます。

空の Review.kt ファイルと右の出力端子を使って、変数やデータ型の理解を深め、Kotlin のコードを書く練習をしてみてください。

## Instructions

ここでは、新しい知識を実践するための方法をいくつか紹介します。

- 好きな曲の名前を String 変数に宣言します。
- Int 変数を宣言して、曲の分単位の長さを指定します。
- ブール型変数を宣言し、好きな曲を聴いているかどうかに応じて true か false を代入します。
- これらの値をターミナルに出力します。

これらの変数のうち、どちらを mutable か immutable かを考えてみましょう。
指定した型で宣言している場合は、型を省略してコードを短くしてみてください。

```kotlin
fun main() {
  // Write your code below
  val songName: String = "Someday the boy"
  val songDuration = 3.56
  var listening: Boolean = false

  if (listening) {
    println("I'm listening " + songName)
    println("Who cares about duration (" + songDuration + ")?")
  } else {
    println("I'm not listening")
  }
}
```
