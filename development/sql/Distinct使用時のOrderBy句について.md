# Distinct 使用時の OrderBy 句について

## 概要

SQL において重複行を取り除く方法の一つして Distinct があるが、この Distinct と OrderBy を併用した際にエラーが発生しハマったので解決方法を残しておく。

## 詳細

### 事象

例えば、簡単に以下のようなテーブルがあるとする。</br>
また、このテーブルには仮想データとしてユニークな ID に紐づく重複が含まれる名前と場所が存在すると仮定する。

| Name       |
| ---------- |
| ID         |
| NAME       |
| PLACE      |
| CREATED_AT |
| UPDATED_AT |

上記のテーブル定義と仮想データから重複を除いた名前と場所を作成時間の昇順でソートした結果を取得しようとして以下の SQL を実行すると失敗する。</br>
※ テーブル名は「DUMMY_TABLE」とする。

```sql
select distinct
    NAME,
    PLACE
from
    DUMMY_TABLE
order by
    CREATED_AT
;
```

しかし、以下のように Distinct を使用しない SQL ではエラーが発生せず結果を取得できる。

```sql
select --distinct
    NAME,
    PLACE
from
    DUMMY_TABLE
order by
    CREATED_AT
;
```

### 原因

**_Distinct と OrderBy を同時に使う場合は必ず Select するカラムを OrderBy に指定しなければいけない_**

調べてみたところ、処理実行後のソート順を保証するために Distinct を使用する場合には、OrderBy に指定するカラムは必ず Select で取得するカラムを指定しなければいけないということがわかった。

SQL ではまず OrderBy の処理が実行され、その後に Distinct で重複行を除去する処理が実行される都合上、Select されていないカラムを OrderBy で指定できるようにしてしまうと Distinct が評価された際に意図しないソートが発生するためらしい。

なるほど、考えてみれば納得の理由だ。
ただ[こちらの記事](https://tmotooka.hatenablog.jp/entry/2012/10/28/085400)によると MySql では上記のエラーを素通りして動いてしまうらしい。

### 解決方法

いくつか解決方法を考えてみたので例を残しておく。

#### そもそも OrderBy はやめる

そのソート処理が必要なのであれば他の方法を検討すべきだが、ソートが必要ないのであればこれが一番簡単な解決方法。

```sql
select distinct
    NAME,
    PLACE,
    CREATED_AT
from
    DUMMY_TABLE
;
```

#### OrderBy で指定するカラムを Select に含める

ただし、この場合にカラムによっては本来意図する結果を取得できない場合がある。

```sql
select distinct
    NAME,
    PLACE,
    CREATED_AT
from
    DUMMY_TABLE
order by
    CREATED_AT
;
```

#### GroupBy を使う

そもそもこういう SQL を書く時は GroupBy を使うべきなのではないだろうか。

```sql
select
    NAME,
    PLACE
from
    DUMMY_TABLE
group by
    CREATED_AT,
    NAME,
    PLACE
;
```

### 結論

Distinct と OrderBy を併存させる際の注意点がよくわかったが、そもそもの話として重複を除いてソートもするといった処理は GroupBy を使うのが手っ取り早そう。
