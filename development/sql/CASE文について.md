# CASE 文について

- [CASE 文について](#case-文について)
  - [概要](#概要)
  - [詳細](#詳細)
    - [構文](#構文)
    - [SELECT 句で CASE 文を使用する](#select-句で-case-文を使用する)
    - [WHERE 句で CASE 文を使用する](#where-句で-case-文を使用する)
    - [SELECT 句で実行した CASE 文の結果を WHERE 句で使用する](#select-句で実行した-case-文の結果を-where-句で使用する)

## 概要

`SQL` における条件分岐は `CASE文` で実現可能であり、
この条件分岐の方法を知っているか知らないかで `SQL` での表現方法に大きな違いが出てくる。

そのため、`SQL` における `CASE文` を使用した条件分岐の方法を整理しておく。

> **_Note:_**</br>
> CASE 文 は `Oracle 9i` 以降で使用が可能。

## 詳細

### 構文

以下の構文を守れば基本的にどのような場面でも使用できる。

```sql
CASE WHEN SOMETHING = 'something' THEN 1 ELSE 0 END
CASE WHEN SOMETHING = 'something' THEN 1 WHEN SOMETHING = 'something' THEN 1 ELSE 0 END
```

1. 必ず `CASE WHEN` から始まる
2. 上記の `SOMETHING = 'something'` のような評価分が続く
3. 評価の真偽値に応じて返却する値を定義
   1. 例えば上記の場合に `SOMETHING` カラムの値が `'something'` であった場合は `1` が返り、そうでない場合は `0` が返る
4. 複数条件にする場合は `THEN` の直後で `WHEN` を書く
5. 必ず `END` で終わる

> **_Note:_**</br>
> 盲点なのは `END` で、これを指定しないと実行時に Oracle エラーが発生する。

### SELECT 句で CASE 文を使用する

`SELECT` 句に CASE 文を書くことでカラム選択時での条件分岐を実現できる。

```sql
select
  CASE WHEN 1 = 1 THEN 'success!' ELSE 'never happen...' END TEST_CASE
from
  dual
;
```

以下のように評価された結果としてカラムの値を加工して返却することもできる。

```sql
select
  CASE WHEN TEST_COLUMN IS NOT NULL THEN TEST_COLUMN || 'test' ELSE '' END TEST_CASE
from
  TEST_TABLE
;
```

### WHERE 句で CASE 文を使用する

`WHERE` 句においても同様に CASE 文を使用することができる。

```sql
select
  TT.*
from
  TEST_TABLE TT
  LEFT OUTER JOIN TEST_NEW_TABLE TNT ON TT.ID = TNT.ID
  LEFT OUTER JOIN TEST_OLD_TABLE TOT ON TT.ID = TOT.ID
where
  1 = 1
  AND TT.TEST_COLUMN = CASE WHEN TOT.TEST_COLUMN IS NOT NULL THEN TOT.TEST_COLUMNELSE TNT.TEST_COLUMN END
;
```

### SELECT 句で実行した CASE 文の結果を WHERE 句で使用する

基本的に以下のような処理はできない。

```sql
select
  CASE WHEN TEST_COLUMN IS NOT NULL THEN TEST_COLUMN || 'test' ELSE '' END TEST_CASE
from
  TEST_TABLE
where
  TEST_COLUMN_2 = TEST_CASE
;
```

しかし、SELECT 句で実行した CASE 文の実行結果は副問合せとすることで使用することができる。

```sql
select
  *
from
  (
    select
      CASE WHEN TEST_COLUMN IS NOT NULL THEN TEST_COLUMN || 'test' ELSE '' END TEST_CASE
    from
      TEST_TABLE
    where
      TEST_COLUMN_2 = TEST_CASE
  )
where
  TEST_CASE = 'somethingtest'
;
```
