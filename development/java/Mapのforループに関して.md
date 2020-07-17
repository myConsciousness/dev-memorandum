# 前段

この記事では実装を問わず Map に格納されたキーと値を繰り返し処理の中で取得するいくつかの方法を紹介します。この記事における読者の対象は主に初級者〜中級者の方です。

プログラミングをする際にまとまった情報を管理する方法として `ArrayList` や `LinkedList` といったリストのデータ構造を使用する場面が多いと思いますが、Map のデータ構造を使いこなすことでより複雑な問題を簡単に扱えるようになりますので、ぜひとも使い方を覚えてほしいと思います。

## 主な取得方法

主に Map 構造のコレクションからキーや値を繰り返し処理で取得するためには以下の方法があります。

- `EntrySet` を使用する
- `forEach()` メソッドを使用する (JDK 1.8 以降)

# EntrySet を使用する方法

今となってはあまり見慣れない方法かもしれませんが、 `EntrySet` を使用することで Map に格納されたキーと値を繰り返し処理の中で簡単に取得することができます。

サンプルコード:

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;

public final class TestEntrySet {

    public static main(String[] args) {
        final Map<String, String> testMap = new HashMap<>();
        testEntrySet.put("test1", "value1");
        testEntrySet.put("test2", "value2");
        testEntrySet.put("test3", "value3");

        final Set<Entry<String, String>> tesEntrySet = testMap.entrySet();

        for (Map.Entry<String, String> entry : testEntrySet) {
            System.out.println(entry.getKey());
            System.out.println(entry.getValue());
        }
    }
}
```

上記サンプルコードでは `HashMap` で実装したテスト用の Map を宣言し、テスト用の値を設定した後で `entrySet()` メソッドを呼び出しています。

`entrySet()` メソッドを呼び出すことで `Set<Entry<String, String>>` 型の `EntrySet` を取得することができます。ここで取得した `EntrySet` を拡張 for 文で使用します。もちろん、上記のサンプルコードでは繰り返し処理の前に `EntrySet` を取得していますが、以下のように拡張 for を使用する際に `EntrySet` を取得することもできます。

```java
// 拡張for文定義時にEntrySetを取得
for (Map.Entry<String, String> entry : testMap.entrySet()) {
}
```

繰り返し処理の中で `getKey()` メソッドを使用することで Map に格納されたキーを、 `getValue()` メソッドを使用することで Map に格納された値を取得することができます。

そのため、上記サンプルコードの実行結果は以下のように出力されます。

```
test1
value1
test2
value2
test3
value3
```

# forEach メソッドを使用する方法

もしかすると、先に紹介した `EntrySet` を使用した繰り返し処理よりもこちらの `forEach()` メソッドを使用した方法のほうが今は主流なのかもしれません。この `forEach()` メソッドは JDK1.8 で関数型インターフェースの追加に伴い実装された比較的新しいメソッドで、`EntrySet` よりも繰り返し処理を直感的に操作することができるようになりました。

```java
import java.util.HashMap;
import java.util.Map;

public final class TestEntrySet {

    public static main(String[] args) {
        final Map<String, String> testMap = new HashMap<>();
        testEntrySet.put("test1", "value1");
        testEntrySet.put("test2", "value2");
        testEntrySet.put("test3", "value3");

        // 引数としてBiConsumer<T, U>を実装するラムダ式を渡す
        testMap.forEach((key, value) -> {
            System.out.println(key));
            System.out.println(value);
        });
    }
}
```

一目見ただけでも `EntrySet` を使用した方法よりも簡潔な書き方であることがわかると思います。

難しそうに見える点は引数ですが、 `forEach()` メソッドの引数には関数型インターフェースである `BiConsumer<T,U>` を実装するラムダ式を渡します。ラムダ式や関数型インターフェースに関してはこの記事の趣旨とズレるので割愛しますが、Map で `forEach()` メソッドを使用する際には上記サンプルコードの書き方を覚えておけば大丈夫です。

ラムダ式で指定する変数名は任意で変更可能で、上記サンプルコードの場合ですと `key` には Map のキーが、 `value` には Map の値が格納されます。

そのため、上記のサンプルコードの実行結果は `EntrySet` を使用したときと同様に以下のようになります。

```
test1
value1
test2
value2
test3
value3
```

## 注意点

上記のサンプルコードを見て気がついた方もいるかもしれませんが、`forEach()` メソッドを使用した繰り返し処理の中では返却値を返すことができません。

例えば、繰り返し処理の中でエラーを検知したら真偽値として `false` を返却したいといったような場合では `forEach()` ではなく `EntrySet` を使用した方法をおすすめします。
