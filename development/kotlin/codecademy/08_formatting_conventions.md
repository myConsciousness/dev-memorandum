# Formatting Conventions

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

プログラミングにおいて、 **_フォーマット規約_** とは、特定のプログラミング言語でコードがどのように構成されるべきかについて提案されたルールのことです。
Kotlin のフォーマット標準、つまりコーディング規約に従うことで、 **_プログラムの可読性を大幅に向上させることができます。_**

Kotlin のフォーマット規約には以下のようなものがあります。

- **_インデント_**

中括弧内のコードは 4 スペースのインデントが必要です。Codecademy のコードエディタでは一般的にインデントに 2 スペース、または 1 タブを使用していますが、`Kotlin` のコードをオフプラットフォームで書く場合は必ず 4 スペースを使用してください。

```kotlin
fun main() {
    // Code starts here
}
```

プログラムにインデントを入れなかった場合でも、コードはエラーなく実行されますが、コードは巨大なテキストの塊のように見えて読みづらくなります。
プログラムが大きくなり、複雑になるにつれ、整理のためのインデントはより重要になってきます。

- **_コメント_**

コメントを書くときは、 `//` とコメントの先頭の間にスペース `(" ")` を入れてください。

```kotlin
// Write your comment here
```

- **_波括弧_**

`main()` 関数を作成する際には、オープニングの中括弧 `{` を `main()` 関数のコンストラクタ (この場合は fun main()) と同じ行に配置してください。閉じ括弧 `}` は別の行に配置し、`fun` キーワードと垂直に並べる必要があります。

```kotlin
fun main() {
  // Code goes here
}
```

このコースやオフプラットフォームで Kotlin のコードを書く際には、上記の規約を心に留めておいてください。このコースを進めていくうちに、より多くの書式規則に出会うことになるでしょう。詳しくは [Kotlin の言語ガイドのコーディング規約](https://kotlinlang.org/docs/reference/coding-conventions.html#formatting)をご覧ください。

## Instructions

```kotlin
fun main()
{
  //        Organize the code below
    println("Down by the bay")
println("Where the watermelons grow,")
              println("Back to my home")
      println("I dare not go.");
         println("For if I do");
 println("My mother will say")
     println("Did you ever use an app that taught you how to snap?")
println("Down by the bay!")
     }
```

上記のコードを見てください。

フォーマットされていませんが、エラーは出ません。
異なるコーディング規約を使用してコードをフォーマットするために時間をかけてください。

次へ進む準備ができたら、次へ をクリックします。

**_出力:_**

```txt
Down by the bay
Where the watermelons grow,
Back to my home
I dare not go.
For if I do
My mother will say
Did you ever use an app that taught you how to snap?
Down by the bay!
```
