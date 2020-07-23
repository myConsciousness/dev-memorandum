# 前段

`Kotlin` はプログラマーによって、プログラマーのために作られた新しいモダンなプログラミング言語です。明快さ、簡潔さ、コードの安全性に重点を置いています。

# 堅牢なコード

`Kotlin` の開発者は、プログラマが無駄のないコードを作成するのを助けるために、言語について様々な設計上の決定を行いました。例えば、ソフトウェアにおける `NullPointerException` の例外は、金銭的損失やコンピュータのクラッシュの原因となり、数え切れないほどの時間をデバッグに費やしてきました。`Kotlin` では、`NULL可能なデータ型` と `NULL可能ではないデータ型` を区別することで、コンパイル時のエラーをより多くキャッチできるようにしています。

`Kotlin` は強力な型付けを行っており、コードから型を推測するために多くのことを行っています。`Kotlin` にはラムダ、コルーチン、プロパティがあり、より少ないコードをより少ないバグで書くことができます。

# 成熟したプラットフォーム

`Kotlin` は 2011 年から存在し、2012 年にオープンソースとしてリリースされました。2016 年にバージョン 1.0 に達し、2017 年からは `Kotlin` が `Android` アプリを構築するための公式サポート言語となっています。`Android Studio 3.0` 以降と同様に `IntelliJ IDEA` に含まれています。

# 簡潔で読みやすいコード

`Kotlin` で書かれたコードは非常に簡潔で、ゲッターやセッターなどの冗長なコードを排除するように設計されています。例えば、次のような `Java` のコードを考えてみましょう。

```java
public class Aquarium {

   private int mTemperature;

   public Aquarium() { }

   public int getTemperature() {
       return mTemperature;
   }

   public void setTemperature(int mTemperature) {
       this.mTemperature = mTemperature;
   }

   @Override
   public String toString() {
       return "Aquarium{" +
               "mTemperature=" + mTemperature +
               '}';
   }
}
```

このコードは `Kotlin` で次のように書くことができます。

```kotlin
data class Aquarium (var temperature: Int = 0)
```

簡潔さと読みやすさという目標は時に相反するものです。`Kotlin` は、簡潔さを保ちながら読みやすさを確保するために、`"必要最低限の定型文コード (just enough boilerplate code)"` を使用するように設計されています。

# Java との相互運用性

`Kotlin` コードはコンパイルされるので、`Java` と `Kotlin` コードを並行して使うことができ、過去に作成したお気に入りの `Java` ライブラリを使い続けることができます。既存の `Java` プログラムに `Kotlin` コードを追加することもできますし、プログラムを完全に移行したい場合は、`IntelliJ IDEA` と `Android Studio` の両方に、既存の `Java` コードを `Kotlin` コードに移行するためのツールが含まれています。
