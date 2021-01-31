# Kotlin におけるリスト構造について

## 概要

初めて `Kotlin` を使用した開発作業中に Java と同じ感覚でリスト構造を使おうとしたら 1 時間程度ハマったので、事象と原因から解法までをまとめておく。

## 事象

`List型` として宣言して `mutableListOf` 関数でリストを初期化したのに値の追加ができない。

```kotlin
    val contentItems: List<ContentItem> = mutableListOf()

    // 可変で初期化したのになぜか add 関数を使えず1時間ほど頭を抱える
    contentItems.add(contentItem)
```

> **_Note:_**</br>
> 上記の事象は今となっては自明のことだが、いきなり Java 畑からやってきてハマる人は多いんじゃないかと思う。
> いや、いてくれ。

## 原因

Kotlin のリスト構造には `不変リスト（List）` と `可変リスト（MutableList）` が存在するが、
上記の事象発生時のように変数の型を明示的に書く場合は `List` と `MutableList` も使い分けないといけない。

## 解法

上記の原因を考慮してコードを修正すると以下のようになる。

```kotlin
    val contentItems: MutableList<ContentItem> = mutableListOf()
    contentItems.add(contentItem) // できた！
```

また、型推論に型の解決を任せる場合は上記の明示的な型指定は不要で `listOf` や `mutableListOf` を呼び出せばいい。

```kotlin
    val contentItems = mutableListOf()
    contentItems.add(contentItem)
```

## まとめ

- `Kotlin` において `List` はリスト共通のインターフェースではない

- コレクションを使用して明示的に型指定する場合は対応した不変・可変の型を指定する

- 型推論に型の解決を任せる場合は不変・可変のコレクションでコレクションを初期化すればいい

こんな感じでまとめておいて思ったのだが、
もしかすると上記のような例では可変リストが使用されることは自明であるから、
`Kotlin` ではこのような場合は明示的な型は指定しないで型推論で書いていくスタイルが多いのだろうか。
