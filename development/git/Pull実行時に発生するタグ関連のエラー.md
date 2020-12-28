# Pull 実行時に発生するタグ関連のエラーについて

## 概要

ローカルで `Pull` コマンドを実行した際に以下のタグ関連の `Git Error` が発生したので調べた対処方法を残しておく。

なぜローカルのタグとリモート先のタグの整合性がとれなくなったのかは不明だが、一先ず解決策は存在する。

```git
> git pull --tags origin master
From https://github.com/myConsciousness/java-generator-commons
 * branch            master     -> FETCH_HEAD
 ! [rejected]        v1.0.0     -> v1.0.0  (would clobber existing tag)
 ! [rejected]        v1.0.1     -> v1.0.1  (would clobber existing tag)
```

## 方法

### 1. ローカルのタグ情報を更新する

以下の `Gitコマンド` を実行しリモート先のタグ情報を取得しローカルのタグ情報を更新する。

```git
git fetch --tags -f
```

以下のように出力されれば OK。

```git
shinya@katoushinyanoMacBook-Pro java-generator-commons % git fetch --tags -f
From https://github.com/myConsciousness/java-generator-commons
 t [tag update]      v1.0.0     -> v1.0.0
 t [tag update]      v1.0.1     -> v1.0.1
```

### 2. `Pull` コマンドを実行する

上記の更新作業が上手く行っていれば再度 `Pull` コマンドを実行した際にエラーが出なくなっている。
