# 前段

実際に `Kotlin` を使用して文字列の `Hello World` を出力する簡単なプログラムを作成してみましょう。

# Hello World!

`ターミナルウィンドウ` で `kotlin` と入力し `Kotlin REPL` を起動してください。

```
$ kotlin
Welcome to Kotlin version 1.3.72 (JRE 1.8.0_131-b11)
Type :help for help, :quit for quit
>>>
```

起動した `Kotlin REPL` 画面に以下のコードを入力してください。

```kotlin
fun printHello() {
    println("Hello World")
}
```

この `Kotlin` のコードをざっと見てみましょう。

`fun` キーワードは関数を指定し、その後に関数名が続きます。他のプログラミング言語と同様に、括弧は関数の引数（もしあれば）を表し、中括弧は関数のコードを表しています。関数は何も返さないので、戻り値の型はありません。また、行末にセミコロンがないことにも注意してください。

`Kotlin REPL` 画面で上記コードで定義した関数を呼び出すと以下のように出力されます。

```kotlin
>>> fun printHello() {
...     println("Hello World")
... }
>>>
>>> printHello()
Hello World
>>>
```

> **Note:** <br>Java 等で行末にセミコロンを入れることに慣れていても問題ありません。Kotlin は行末のセミコロンを意識しません。
