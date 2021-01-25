# Declaring A Mutable Variable

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

変数の概念を理解したところで、`Kotlin` で変数を作成する方法を学びましょう。
完全な変数の宣言と初期化は以下のような形になります。

```kotlin
var variableName: Type = value
```

- **_宣言_**

`var` キーワードは、変数宣言の先頭を指定します。
これは、プログラム中で値が変化する可能性があることを意味する `ミューターブル変数` を意味します。

キーワードの後には、キャメルケース形式の変数名が続きます。
キャメルケースとは、最初の単語を小文字にし、2 番目の単語の最初の文字を大文字にする命名規則のことです。

可読性と保守性のためには、簡潔でありながら説明的な変数名を作成することが重要です。
ある有名なソフトウェアエンジニアが次のように言っていました。

`"私は、自分のコードを読みやすくするために、変数名やメソッド名などの識別子名に文字通り何時間も費やすことになるだろう...」 - Joshua Bloch`

変数名の後には、その変数が格納するデータの型が続きます。

- **_初期化_**

変数が宣言されたら、値で初期化することができます。
プログラミングでは代入演算子として知られる `=` 記号は、変数に値を代入します。

この構文を最初の Kotlin 変数に適用してみましょう。
型は常に大文字でなければなりません。

```kotlin
var guitarName: String = "Fender Stratocaster"
```

guitarName 変数は、コンパイラによってメモリ上の位置が割り当てられ、プログラム全体で参照して使用することができるようになりました。

コンパイラは、変数名の前に `var` キーワードがあることで、この変数が可変であることを認識しています。

プログラムの中で変数を宣言する必要がある場合がありますが、その変数を初期化するための値がない場合があります。このような場合は、次のようにして宣言することができます。

```kotlin
var variableName: Type
```

ギターで演奏された音を聞く音楽アプリケーションを作っているとしましょう。
notePlayed 変数を宣言して、ユーザーが音符を弾いたときに値を初期化することができます。

```kotlin
var notePlayed: String // declaration
notePlayed = "B" // initialization
println(notePlayed) // Prints: B
```

上記コードの 2 行目に `var` キーワードを使用する必要がなかったことに注目してください。
また、この情報は一度だけ指定する必要があるので、データの型も省略しています。

## Instructions

### 1. Date.kt の main()関数内で、todaysDate という名前の String 変数を宣言し、mm/dd/yyyy 形式で今日の日付で初期化します

```kotlin
fun main() {
  // Write your code below ☀️
  var todaysDate: String = "01/25/2021"
  println(todaysDate)
}
```

**_出力結果_**

```txt
01/25/2021
```

### 2. 次の行で、別の String 変数 currentWeather を宣言してください

```kotlin
fun main() {
  // Write your code below ☀️
  var todaysDate: String = "01/25/2021"
  println(todaysDate)

  var currentWeather: String;
  currentWeather = "Sunny"
  println(currentWeather)
}
```

**_出力結果_**

```txt
01/25/2021
Sunny
```
