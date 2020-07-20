# 前段

この記事では実装を問わず `List` のデータ構造を使用した繰り返し処理の操作方法をいくつか紹介します。

記事の内容に関しては普段から Java を使用してプログラミングを行っている方からすれば常識レベルのことなので、読者の対象は Java を学び始めた初心者を想定しています。しかし、JDK 1.8 で追加された `forEach` メソッドを使用した繰り返し処理に関しては未だに開発現場でも使用している方が少ない印象なので、この際に `forEach` メソッドの使い方に関しても覚えてほしいと思います。

なお、この記事では List コレクションを用いた単純な繰り返し処理を扱うため、`filter` といった中間操作を行う `Stream API` には触れません。`Stream API` に関してはまた別の記事で紹介できればと考えています。

## この記事を読むことでできるようになること

- List コレクションを使用した繰り返し処理

## 主な繰り返し処理の操作方法

- `get(int)` メソッドを使用したランダムアクセス
- `拡張for文` を使用したシーケンシャルアクセス
- `forEach(Consumer<T>)` メソッドを使用したシーケンシャルアクセス (JDK 1.8 以降)

# `get` メソッドを使用したランダムアクセス

`拡張for文` や JDK 1.8 で `forEach` メソッドといった便利かつ効率的な機能が登場してからは List コレクションに対して `get` メソッドを使用しランダムアクセスで繰り返し処理を行うという場面はほとんどなくなりました。しかし、このランダムアクセスは実装を問わず List コレクションを用いた最も基本的な繰り返し処理の方法ですので、Java を使ってプログラミングをする方には必ず覚えておいてほしいです。

基本的な操作方法は以下のようになります。

```java
import java.util.List;
import java.util.ArrayList;

public final class TestGet {

    public static void main(String[] args) {
        final List<String> testList = new ArrayList<>(3);
        testList.add("test1");
        testList.add("test2");
        testList.add("test3");

        for (int i = 0, size = testList.size(); i < size; i++) {
            // 変数i番目の要素を取得（ランダムアクセス）
            System.out.println(testList.get(i));
        }
    }
}
```

上記のサンプルコードではまず 3 つの要素を格納することができるテスト用の List を `ArrayList` として実装し、テスト用の値を `add` しています。

その後は基本的な for 文を使用し、先に用意した `testList` のサイズ分だけ処理を繰り返します。上記のサンプルコードですと繰り返し処理の度に変数 `i` はインクリメントされていきますので、コメントにもあるように `testList.get(i)` の処理は `testList` の要素に対して順次にランダムアクセスしていくものになります。

そのため、上記のサンプルコードの実行結果は以下のように出力されます。

```
test1
test2
test3
```

## 注意点

1. ### ランダムアクセスを行う際にはアクセス可能な範囲を必ず明確にする

上記のサンプルコードのように `get` メソッドを使用したランダムアクセスを使用する場合は必ずアクセス対象の List のサイズを確認してください。もし `get` メソッドに対象 List のサイズよりも大きいインデックスを指定した場合は実行時に必ず `IndexOutOfBoundsException` （範囲外例外）が発生し処理が失敗します。

例えば、以下のような場合です。

```java
import java.util.List;
import java.util.ArrayList;

public final class TestIndexOutOfBoundsException {

    public static void main(String[] args) {
        final List<String> testList = new ArrayList<>();
        testList.add("test1");
        testList.add("test2");
        testList.add("test3");

        // 存在しない4個目のインデックスを指定
        testList.get(3);
    }
}
```

上記のサンプルコードを実行すると以下の例外が発生します。

```
java.lang.IndexOutOfBoundsException: Index 3 out of bounds for length 3
    at java.base/jdk.internal.util.Preconditions.outOfBounds(Preconditions.java:64)
    at java.base/jdk.internal.util.Preconditions.outOfBoundsCheckIndex(Preconditions.java:70)
    at java.base/jdk.internal.util.Preconditions.checkIndex(Preconditions.java:248)
    at java.base/java.util.Objects.checkIndex(Objects.java:373)
    at java.base/java.util.ArrayList.get(ArrayList.java:425)
```

ランダムアクセスを行う対象の List のサイズは先の正常終了するサンプルコードにもあるように `size()` メソッドで取得できます。なお、データベースから一意のキーをもとに一つのレコードのみが必ず取得できるといったような場合では、`size()` メソッドで List のサイズを検査せずに `testList.get(0);` といった処理で対象の値を取得することは認められます。

重要な点は、ランダムアクセスを行う際には `IndexOutOfBoundsException` が実行時に発生しないようにアクセス可能な範囲を明確にすることです。

2. ### `LinkedList` に対するランダムアクセスは極力避ける

Java の List コレクションの中には `LinkedList` という `ArrayList` 同様によく使われるデータ構造が存在します。この `LinkedList` は格納した要素同士の前後関係をリンクで保持する仕組みから、配列に新しく要素を挿入することや配列内の要素を削除する処理に適したデータ構造になります。

しかし、`LinkedList` に対するランダムアクセスはパフォーマンスが最悪です。ランダムアクセスする要素数が 100 件程度であれば `ArrayList` 使用時とほとんど変わらない処理時間になりますが、`LinkedList` で 10 万件以上の規模の大きいデータに対してランダムアクセス繰り返し処理を行うことはパフォーマンスの面から現実的ではありません。

そのため、`LinkedList` で規模の大きいデータを繰り返し処理で扱う際には、`get` メソッドを使用したランダムアクセスではなく、後に紹介する `拡張for文` や `forEach` メソッドといったシーケンシャルアクセスで操作を行ってください。

## 余談

ランダムアクセスに関して以下のサンプルコードを先に紹介しました。

```java
import java.util.List;
import java.util.ArrayList;

public final class TestGet {

    public static void main(String[] args) {
        final List<String> testList = new ArrayList<>(3);
        testList.add("test1");
        testList.add("test2");
        testList.add("test3");

        for (int i = 0, size = testList.size(); i < size; i++) {
            // 変数i番目の要素を取得（ランダムアクセス）
            System.out.println(testList.get(i));
        }
    }
}
```

もしかしたら、上記のサンプルコードの for 文が初心者の方には見慣れない書き方なのではないかと思いましたので説明を残しておきます。
上記のサンプルコードですが for 文の部分は以下のように書くことができます。

```java
for (int i = 0; i < testList.size(); i++) {
    // do something
}
```

条件式部分で `size()` メソッドを実行し `testList` のサイズを取得するようにしてみました。

しかし、上記の for 文の書き方は避けるべきです。なぜなら、for 文の条件式部分 `i < testList.size()` は繰り返し処理の度に実行されるため、上記コードの場合ですと `testList` のサイズ分だけ `size()` メソッドが呼び出されることになります。10 件や 100 件程度であればパフォーマンスに影響はほとんど無いですが、それでも小さな差も積もれば大きな差になります。

例えば、以下のようなサンプルコードで条件式部分の処理が毎回実行されていることを確認することができます。

```java
public final class Main {

    public static void main(String[] args) throws Exception {
        // 条件式部分が毎回実行されていることを確認
        for (int i = 0; i < 10 && saySomething(); i++) {
            // do something
        }
    }

    private static boolean saySomething() {
        System.out.println("Hello World!");
        return true;
    }
}
```

上記のサンプルコードの実行結果は以下のように出力されます。普段の開発で上記のようなコードを書くことはないですが、条件式部分の `saySomething()` メソッドが 10 回実行されていることを確認できました。

```
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
```

以上から、for 文開始時に 1 回だけ実行される初期化式部分で条件式部分で使用する件数を求めておくことで、無駄のないより効率的なプログラムを書くことができます。これは List コレクションにおける `size()` メソッドに限らず多様な場面で応用できるテクニックですので、より良いプログラムを目指す方々にはぜひとも日々心がけるようにしていただきたいです。

## `拡張for文` を使用したシーケンシャルアクセス

`拡張for文` が Java の機能として追加されたからしばらく経ち、既に List コレクションの順次繰り返し処理ではデファクトスタンダードな書き方になりました。for 文の書き方もランダムアクセス時のものより簡潔で効率的なものになっています。

`拡張for文` が導入される以前は `Iterator` インターフェースを実装することでシーケンシャルアクセスを実現していました。`Iterator` インターフェースでのシーケンシャルアクセスは実装する処理が複雑でかつ多く、既にレガシーな書き方で使用する場面もほとんどないのでこの記事では扱いませんが、知識として `拡張for文` の登場以前には `Iterator` インターフェースを使用してシーケンシャルアクセスを実現していたと頭の片隅に置いておいてください。

また、`get` メソッドを使用したランダムアクセス時に紹介した　`IndexOutOfBoundsException` （範囲外例外）や　`LinkedList` 使用時のパフォーマンス劣化は、`拡張for文` を使用したシーケンシャルアクセスでは発生しません。

JDK1.8 までは List に格納された値を逆から取得するという特殊な場合にランダムアクセスでの for 文処理を行うことがありましたが、JDK1.8 で `Stream API` 導入に伴い `reverse()` メソッドといったコレクション操作のための便利な機能が追加されているため、ランダムアクセスで繰り返し処理を書く場面は本当に少なくなりました。

そのため、`拡張for文` を使用できる場面であればランダムアクセスでの繰り返し処理は行わず、`拡張for文` を使用した繰り返し処理を書くように心がけてください。

さて、先に紹介した `get` メソッドを使用したランダムアクセスのサンプルコードを `拡張for文` を使用したシーケンシャルアクセスで書き直すと以下のようになります。

```java
import java.util.List;
import java.util.ArrayList;

public final class TestEnhancedForStatement {

    public static void main(String[] args) {
        final List<String> testList = new ArrayList<>(3);
        testList.add("test1");
        testList.add("test2");
        testList.add("test3");

        for (String value : testList) {
            // testListに格納された値を先頭から順に取得
            System.out.println(value);
        }
    }
}
```

上記サンプルコードの `拡張for文` の読み方としては、「`testList` に格納された値を先頭から順番に `String` 型の値として取得して変数名 `value` に格納する」という感じになります。他の Python や Ruby といった高級言語でも同じような文法なので、他の高級言語を既に触れている方すれば特に難しい点はないと思います。

そして、上記のサンプルコードを実行した出力結果は以下のようになります。

```
test1
test2
test3
```

## `forEach` メソッドを使用したシーケンシャルアクセス

JDK1.8 にて関数型インターフェースの導入に伴い、List コレクションを繰り返し処理で操作する `forEach(Consumer<T>)` メソッドが追加されました。このメソッドは以前私が Map コレクションに関する繰り返し処理に関して書いた記事で紹介した `forEach(BiConsumer<T,U>)` メソッドによく似た機能になります。`拡張for文` よりもさらに簡潔で直感的にシーケンシャルアクセスの処理を書くことができるようになりました。

基本的な書き方は以下のようになります。

```java
import java.util.List;
import java.util.ArrayList;

public final class TestForEach {

    public static void main(String[] args) {
        final List<String> testList = new ArrayList<>(3);
        testList.add("test1");
        testList.add("test2");
        testList.add("test3");

        testList.forEach((value) -> {
            // testListに格納された値を先頭から順に取得する
            System.out.println(value);
        });
    }
}
```

難しそうに見える点は引数ですが、 `forEach()` メソッドの引数には関数型インターフェースである `Consumer<T>` を実装するラムダ式を渡します。`Consumer<T>` は 1 つだけ引数を貰ってなにも値を返却しない操作を抽象化した関数型インターフェースです。

ラムダ式や関数型インターフェースに関してはこの記事の趣旨とズレるので割愛しますが、List で `forEach()` メソッドを使用する際には上記サンプルコードの書き方を覚えておけば大丈夫です。

そして、上記のサンプルコードを実行した出力結果は以下のようになります。

```
test1
test2
test3
```

## 注意点

- ### `forEach` メソッドは値を返すことができない

先に関数型インターフェースの説明でも軽く触れましたが、`Consumer<T>` の特性から `forEach` メソッドは値を返すことができません。そのため、List の繰り返し処理中で何らかのエラーを検知した場合は真偽値として `false` を返却したいといった場合には `拡張for文の` 使用を検討してください。
