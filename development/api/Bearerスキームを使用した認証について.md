# 1. Bearer スキームを使用した認証について

<!-- TOC -->

- [1. Bearer スキームを使用した認証について](#1-bearer-スキームを使用した認証について)
  - [1.1. 概要](#11-概要)
    - [1.1.1. 疑問](#111-疑問)
  - [1.2. 詳細](#12-詳細)
    - [1.2.1. Authorization ヘッダについて](#121-authorization-ヘッダについて)
    - [1.2.2. Authorization ヘッダの Bearer スキームとは](#122-authorization-ヘッダの-bearer-スキームとは)
    - [1.2.3. RFC 6750 に準拠した Bearer スキームを実装するためには](#123-rfc-6750-に準拠した-bearer-スキームを実装するためには)
    - [1.2.4. Bearer スキームでないトークン認証手法を選ぶべき状況はあるか](#124-bearer-スキームでないトークン認証手法を選ぶべき状況はあるか)
  - [1.3. まとめ](#13-まとめ)

<!-- /TOC -->

## 1.1. 概要

- HTTP でトークンを利用した認証・認可をする手法として [RFC 6750](http://tools.ietf.org/html/rfc6750) がある
- OAuth に限らず、トークンを利用して認証・認可する機構の一部として `Authorization: Bearer` ヘッダを使うことができる

### 1.1.1. 疑問

- `Authorization: Bearer` ヘッダは OAuth と関係しているらしいけど、ログインに OAuth を使わない API でも使用してもいいのか
- `Authorization` 以外のヘッダでトークンを送る API に倣ったほうがいいのか
  - 例：[GitHub API v3](https://developer.github.com/v3/oauth/#web-application-flow)は `Authorization: token トークン` ヘッダ
  - 例：[AWS Signature v4](http://docs.aws.amazon.com/AmazonS3/latest/API/sigv4-auth-using-authorization-header.html) は `Authorization: AWS4-HMAC-SHA256 トークン他…` ヘッダ
  - 例：[Chatwork API](http://developer.chatwork.com/ja/endpoints.html) は `X-ChatWorkToken: トークン` ヘッダ

## 1.2. 詳細

### 1.2.1. Authorization ヘッダについて

- `Authorization` ヘッダの仕様は [RFC 7235 - Hypertext Transfer Protocol (HTTP/1.1): Authentication](https://tools.ietf.org/html/rfc7235) で定義されている
- `Authorization: auth-scheme (token68 / auth-params)` の形式で書くことが定められている
- 各スキームの仕様については言及されていない
- [RFC 7235 section 5.1](http://tools.ietf.org/html/rfc7235#section-5.1) によれば、 `auth-scheme` の取り得る値は IANA で管理されている
- `Basic`, `Digest` が代表的な登録済みスキーム、 `Bearer` も登録済み
- GitHub や AWS のように独自のスキームを使うよりは `Bearer` スキームの仕様に則ったほうが良い

### 1.2.2. Authorization ヘッダの Bearer スキームとは

- Bearer スキームは [RFC 6750 - The OAuth 2.0 Authorization Framework: Bearer Token Usage](http://tools.ietf.org/html/rfc6750) で定義されている
- RFC 6750 は OAuth 2.0 の認可機構として設計されたものだが、 OAuth に限らず汎用的な HTTP 認可に使用することができる

> While designed for use with access tokens
> resulting from OAuth 2.0 authorization [RFC6749] flows to access
> OAuth protected resources, this specification actually defines a
> general HTTP authorization method that can be used with bearer tokens
> from any source to access any resources protected by those bearer
> tokens. The Bearer authentication scheme is intended primarily for
> server authentication using the WWW-Authenticate and Authorization
> HTTP headers but does not preclude its use for proxy authentication.

- RFC 6750 の要求仕様に従って Bearer スキームを使えばいい

### 1.2.3. RFC 6750 に準拠した Bearer スキームを実装するためには

正確なところは RFC 6750 を参照してもらうとして概略を以下に示す。

- トークンは任意の [token68](http://wiki.suikawiki.org/n/token68) 文字列とする
- 保護されたリソースにアクセスするとき、クライアントは `Authorization: Bearer トークン` ヘッダをリクエストに含めて送信する
- リクエストがアクセス要件を満たさないなら、サーバは `WWW-Authenticate: Bearer パラメータ` ヘッダを返さ _なければならない_
  - パラメータは 1 つ以上必要
    - 特に返したいパラメータがなければ最低限 `realm=""` を入れておけば良い
  - エラーの場合は適切なステータスコードと特定の値の `error` パラメータを返す _べきである_
  - ただし、リクエストが認可のためのヘッダを含まない（つまり認可が必要であることをクライアントが知らない）なら `error` パラメータを含める _べきではない_
  - `error_description` パラメータにエラーを説明する文字列を含め _てもよい_
  - `error_uri` パラメータにエラーを説明するページへの URI を含め _てもよい_
- （リクエストがアクセス要件を満たすときのレスポンスの形式については特に指定されていない）

リクエストがアクセス要件を満たさないときの典型的なレスポンス例は以下のようになる。

- リクエストが Authorization ヘッダを含まない場合
  - 401 Unauthorized
  - ヘッダに `WWW-Authenticate: Bearer realm="適当なrealm"` を含む
- リクエストパラメータが不正な場合
  - 400 Bad Request
  - ヘッダに `WWW-Authenticate: Bearer error="invalid_request"` を含む
- トークンが失効や破損などの理由で不正な場合
  - 401 Unauthorized
  - ヘッダに `WWW-Authenticate: Bearer error="invalid_token"` を含む
- トークンのスコープが不十分な場合
  - （この記事ではスコープについて触れない。詳しくは [RFC 6750 section 3](https://tools.ietf.org/html/rfc6750#section-3) を参照）
  - 403 Forbidden
  - ヘッダに `WWW-Authenticate: Bearer error="insufficient_scope"` を含む

空でない realm を一貫してパラメータに含めたほうが親切かもしれない。
たとえば `realm="token_required"` 等。

> **_Note:_**</br>
> token68 は ASCII アルファベット、 ASCII 数字、 `-`, `.`, `_`, `~`, `+`, `/` からなる文字列（末尾に 0 個以上の `=` があってもよい）。改行を含まない任意の base64 文字列は正しい token68 文字列になる。

### 1.2.4. Bearer スキームでないトークン認証手法を選ぶべき状況はあるか

例えば Basic 認証とトークンによる認証の両方を同時に要求したい場合が考えられる。 `Authorization` ヘッダはリクエスト中に 1 つしか含められないため。（[RFC 7230 section 3.2.2](https://tools.ietf.org/html/rfc7230#section-3.2.2) を参照）

[RFC 7235 section 2.1](https://tools.ietf.org/html/rfc7235#section-2.1) によれば、アプリケーションは HTTP 以外の仕組みによる認証を併せて利用してもよいし、追加の HTTP ヘッダを用いた認証を行なってもよい：

> HTTP does not restrict applications to this simple challenge-response
> framework for access authentication. Additional mechanisms can be
> used, such as authentication at the transport level or via message
> encapsulation, and with additional header fields specifying
> authentication information. However, such additional mechanisms are
> not defined by this specification.

## 1.3. まとめ

- `Authorization: Bearer` ヘッダの仕様は RFC6750 で定められている
- OAuth の仕様の一部だが、 OAuth に限らず一般的な HTTP 認可の手段として使える
- 仕様に準拠するためにはサーバは特定のレスポンスを返さ _なければならない_
- 特に事情がなければ RFC6750 に従って `Authorization: Bearer` ヘッダを使えば良い
