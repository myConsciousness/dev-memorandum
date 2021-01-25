# Print Statements

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

前回の演習では、以下のコードで出力端末に `Coding is fun!` というテキストを表示させることができました。

```kotlin
fun main() {
  println("Coding is fun!")
}
```

私たちは `print文` を使ってこの偉業を成し遂げました。`print文` はターミナルに値を出力します。
`Kotlin` で `print文` を使いたいときは `println()` 関数を使って、出力ターミナルに改行する前に値を出力します。

```kotlin
println("To infinity and beyond!")
```

出力したい値はすべて `println()` の括弧内に入れる必要があります。
テキストを出力したい場合は、テキストを二重引用符("")で囲む必要があります。
上のスニペットのコードは次のように出力されます。

```txt
To infinity and beyond!
```

`print文` を使って、数値や式の結果を出力することもできます。
例えば、以下のようになります。

```kotlin
println(5 + 5)
```

以下のように出力されます

```txt
10
```

このコースでは主に `println()` を使用しますが、値を出力するための別のオプションとして `print()` があります。

`println()` と `print()` の違いは、 `println()` は値を出力した後に改行を行うのに対し、`print()` は改行を行わないことです。
例えば、以下のようになります。

```kotlin
println("One")
print("Two")
print("Three")
```

次のように出力されます。

```txt
One
TwoThree
```

## Instructions

### 1. Print.kt で println()を使って "Just keep swimming!"を出力します

```kotlin
fun main() {
  println("Just keep swimming!")
}
```

**_出力:_**

```txt
Just keep swimming!
```

### 2. Print.kt で print()を使用して 15 \* 4 の式を出力します

```kotlin
fun main() {
  println("Just keep swimming!")
  print(15 * 4)
}
```

**_出力:_**

```txt
Just keep swimming!
60
```
