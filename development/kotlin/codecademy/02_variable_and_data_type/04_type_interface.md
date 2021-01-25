# Type Interface

これは `Codecademy` での `Kotlin学習コース` の要所を抜粋したメモになります。</br>
そのため、「コードエディタ」や「実行ボタン」といった単語が出てきますが、実際に提示された課題を解く場合には実際に `Codecademy` でコースを受講するか自分のローカルマシンに問題と同じソースコードを作成してください。

## Summary

`Kotlin` では、 **_型推論_** と呼ばれる機能を使うことでキーストロークを節約し、変数宣言を最適化することができます。

`型推論` とは、コンパイラが宣言された変数の型を推論し、そのデータ型を宣言の中で省略できることを示しています。
次の変数宣言を見てみましょう。

```kotlin
var lightsOn: Boolean = true
```

変数の型を明示的に記述していますが、`Kotlinコンパイラ` は型がなくてもこのような仮定をすることができるほどに賢いです。

```kotlin
var lightsOn = true // valid declaration
```

コンパイラは、変数に格納された真または偽の値がブール値データ型に該当することを認識します。

変数がどのように宣言されているかにかかわらず、その型はプログラムを通して変更できないことを知っておくことが重要です。
Boolean 変数は、明示的に宣言されていても推測されていても、真か偽の値しか保持できません。

ブール値ではない値を代入しようとすると

```kotlin
lightsOn = "no" // error
```

コンパイラは以下のエラーをスローします。

```txt
Inference.kt:4:14: error: type mismatch: inferred type is String but Boolean was expected
  lightsOn = "no"
```

> **_Note:_**</br>
> 明示的に指定されたデータ型を持つ変数宣言と、推測されるデータ型を持つ変数宣言のどちらも、変数を作成する上で有効な方法です。
> それぞれの構文はコンパイラに受け入れられますので、どちらを選ぶかは開発者の好みによります。

## Instructions

`Inference.kt` では、main()関数の中に print()文と Kotlin コードを追加し、typeTest と呼ばれる変数の推定データ型を出力するようにしました。
このコードがどのように動作するのかを正確に理解することは心配しないでください。
今のところは、コンパイラによって推論されたデータの型を表示するために使用します。

**_print() ステートメントの上で、typeTest を宣言し、このリストの中から任意の値で初期化します。_**

- "6"
- 6
- true
- "false"
- 2.6

コンソールで推論された型を観察してみましょう。
typeTest に他のいくつかの値を割り当ててテストします。

```kotlin
fun main() {
  var typeTest = "false"
  // Declare your variable above ⬆️
  print("${typeTest::class.simpleName}")
}
```

**_出力:_**

```txt
String
```
