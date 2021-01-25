# Declaring An Immutable Variable

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

`Kotlin` に存在するもう一つのタイプの変数として、 `不変変数` があります。
`不変` とは、 **_初期化後に値が突然変異したり変更されたりすることのない変数_** を意味します。

不変変数は `val` キーワードで表され、いくつかの言語では定数と呼ばれることもあります。
以下に、`Kotlin` での宣言方法を示します。

```kotlin
val variableName: Type = value
```

例を見てみましょう。
次の変数には、黄金比の値が格納されています。

```kotlin
val goldenRatio: Double = 1.618
```

この値が定数であることがわかっているので、値を変更するつもりはないので、`var` ではなく `val` キーワードで宣言するのがベストです。
`var` を使った宣言もコンパイラには受け入れられますが、プログラムのどこかで値が変更されることが確実な場合にのみ `var` を使って変数を宣言するのが好ましい方法で、そうでない場合は常に `val` を使用します。

goldenRatio を別の値に代入してみるとどうなるか見てみましょう。

```kotlin
goldenRatio = 3.2
```

上記のコードを実行すると、ターミナルで **_再割り当てが許可されていない_** という以下のエラーが発生します。

```txt
Pi.kt:5:3: error: val cannot be reassigned
  goldenRatio = 3.2
  ^
```

## Instructions

### 1. Pi.kt で不変変数 pi を宣言します

```kotlin
fun main() {
  // Write your code below
  val pi: Double = 3.14
}
```

> **_Note:_**</br>
> この変数は使用されておらず、宣言されているだけなので、この変数が使用されていないことを示す Warning メッセージがコンパイラによってスローされるのがわかります。警告はエラーとは異なり、プログラムの実行を妨げるものではありません。これは Kotlin がプログラムの中に使われていないコードがないことを確認するための方法にすぎません。

### 2. 次の行で、変数名を入力し、別の Double 値を再代入してください

```kotlin
fun main() {
  // Write your code below
  val pi: Double = 3.14
  pi = 3.1415926
}
```

**_出力:_**

```txt
Pi.kt:4:3: error: val cannot be reassigned
  pi = 3.1415926
  ^
```
