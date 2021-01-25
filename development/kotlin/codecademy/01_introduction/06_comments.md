# Comments

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

コードが何を達成しているかを文書化することは良いプログラミングの実践です。

コメントを使うと、プログラムの中に文書を書くことができます。コメントはプログラム全体のどこにでも書くことができ、テキスト、記号、またはコードを含むことができますが、これらはすべてコンパイラによって無視されます。

一行のコメントを書くには、プログラムに // と入力してから、追加したいコメントを入力します。

```kotlin
// To be or not to be: that is the question.
```

`//` はコメントの開始を表します。
コメントに表示されるテキストの色が灰色であることに注意してください。

また、複数行コメントを使用して、複数行に渡ってコメントを書くこともできます。
複数行コメントは `/*` で始まり `*/` で終わります。

```kotlin
/*
If you prick us, do we not bleed?
If you tickle us, do we not laugh?
If you poison us, do we not die?
And if you wrong us, shall we not revenge?

- William Shakespeare, The Merchant of Venice
*/
```

## Instructions

### 1. Comments.kt で以下のテキストを一行コメントとして追加します

```kotlin
fun main() {
  // Code prints "Howdy, partner!" to the terminal.
  println("Howdy, partner!")
}
```

### 2. Kotlin を使ったプログラミングについてこれまでに学んだことを複数行のコメントで記述してください

```kotlin
/*
   Main function
   Print statements
   Order of execution
   Comments
*/

fun main() {
  // Code prints "Howdy, partner!" to the terminal.
  println("Howdy, partner!")
}
```
