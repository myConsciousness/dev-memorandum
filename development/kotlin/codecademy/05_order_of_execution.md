# Order Of Execution

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

レシピの命令と同様に、コードはトップダウンで読み込まれ、コンパイルされ、実行されます。

プログラムを実行すると、コンパイラが `Kotlin` のコードを `Java 仮想マシン（JVM）` が読めるものに変換します。`JVM` はコードを命令として実行する役割を担っています。

これらはすべて、コードを実行してからターミナルで出力を見るまでの間、バックグラウンドで行われます。

`main()関数` の内部では、コードの先頭行がコンパイラによって読み込まれる最初の命令となります。
例えば、3 つの `print文` を含むプログラムを作成してみましょう。

```kotlin
fun main() {
    println("Huzzah!")
    println("Woohoo!")
    println("Yehaw!")
}
```

上のスニペットでは、`"Huzzah!"` を含む `print文` が `main()関数` のコードの最初の行になっているので、最初に `"Woohoohoo!"` の後に `"Yehaw!"` が続いて出力端末に出力されます。

```txt
Huzzah!
Woohoo!
Yehaw!
```

## Instructions

### 1. 1932 年のエミュ大戦争のタイムラインを作成するには、println()を使用します

以下のテキストを使用して、3 つの print 文を作成します。

- "11/2 - AU military goes to war against local emus."
- "11/4 - Ambush planned by military fails."
- "11/8 - AU military withdraws."

```kotlin
fun main() {
    println("11/2 - AU military goes to war against local emus.")
    println("11/4 - Ambush planned by military fails.")
    println("11/8 - AU military withdraws.")
}
```

**_出力:_**

```txt
11/2 - AU military goes to war against local emus.
11/4 - Ambush planned by military fails.
11/8 - AU military withdraws.
```
