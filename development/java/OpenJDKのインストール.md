# OpenJDK をインストールする方法

## やりたいこと

最新の `Open JDK` をインストールしたい。

## 経緯

数年前の `Oracle JDK` の有償化によって `Java 11` 以降を使用する場合は `Open JDK` を使用するのがスタンダードになっているらしいが、インストール方法を調べてみると記事によって書いていることが違ったり、そもそもその手順に沿ってインストールを進めても上手くインストールできなかった。

`「これでは埒が明かない。」`

そう思ってより範囲を広げて調べてみると、環境変数周りも設定してくれる便利なインストーラが付いている `AdoptOpenJDK` というコントリビューションを見つけた。こちらを使用したところ一発で最新の `Open JDK` を導入できたのでその手順を残しておく。

## 方法

### 1. `AdoptOpenJDK` のインストーラをダウンロード

[AdoptOpenJDK](https://adoptopenjdk.net/)のホームページにアクセスすると、`Download for ~` という文言の下に `OpenJDK` のバージョンと `JVM` のバージョンを選ぶラジオボタンがある。

安定版を使いたいのであれば `LTS` と書かれたバージョンを使えばよいが、最新の機能を試してみたかった私は `Latest` と書かれたバージョンを選択した。 `JVM` に関しては専門知識が不足しているので初期値で設定されていた `HotSpot` を選択した。

バージョンを選択して `Latest release` ボタンを押下するとインストーラのダウンロードが始まる。

### 2. ダウンロードしたインストーラからインストール

先の手順でダウンロードしたインストーラをダブルクリックすると見慣れたインストール画面が開く。
基本的に `次へ` ボタンを押していくだけで良い。

### 3. インストールが完了したら `Java` のバージョンを確認（任意）

インストールしたバージョンが反映されているか確認するためにコマンドプロンプトで以下のコマンドを叩く。

```cmd
java -version
```

私の場合は `OpenJDK 14` をインストールしたので以下のような結果を得られる。

```cmd
java -version
openjdk version "14.0.2" 2020-07-14
OpenJDK Runtime Environment AdoptOpenJDK (build 14.0.2+12)
OpenJDK 64-Bit Server VM AdoptOpenJDK (build 14.0.2+12, mixed mode, sharing)
```

## JVM に関する補足

知らないまま放置しておくのもなんなので `HotSpot` と `OpenJ9` について調べてみた。

> 原文:<br>
> ・HotSpot is the VM from the OpenJDK community. It is the most widely used VM today and is used in Oracle’s JDK.<br>
> ・Eclipse OpenJ9 is the VM from the Eclipse community. It is an enterprise-grade VM designed for low memory footprint and fast start-up and is used in IBM’s JDK.

> 訳文:<br>
> ・HotSpot は OpenJDK コミュニティの JVM です。 現在最も広く使用されている JVM であり、 Oracle の JDK で使用されています。<br>
> ・Eclipse OpenJ9 は Eclipse コミュニティーの JVM です。低メモリ使用量と高速起動用に設計されたエンタープライズクラスの JVM であり、 IBM の JDK で使用されています。

メモリ使用量と起動速度に関する性能測定は行っていないが、拘りがなければ基本的には `HotSpot` を使えば問題なさそうだ。
