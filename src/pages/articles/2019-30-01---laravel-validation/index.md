---
title: 【Laravel】バリデーションを拡張する
date: "2019-01-30T12:00:00.169Z"
layout: post
draft: false
path: "/posts/laravel-validation/"
category: "Web Development"
tags:
  - "Web Development"
description: "Laravelには優秀なバリデーション機能が初めから備わってるが、それだけでは足りない場合がある。その場合、独自のバリデーションを作成することができるので、その方法をまとめる。"
---

## extendメソッド

まずは例を書く。

```
Validator::extend('foo', function ($attribute, $value, $parameters, $validator) {
            return $value <= $parameters;
 });
```

解説すると、入力した値が`foo`ならtrue、そうでなければエラーになる。

第一引数の`foo`はバリデーション名。

requiredとかuniqueとかの仲間になる。

emailにバリデーションを追加したい場合は、

```
public function rules()
    {
        return [
            'email' => 'required|email|foo:100,
        ];
    }
```

こんな感じにfooを書く。

そして第二引数はクロージャになるからその引数も1つずつ解説していく。

### $attribute => リクエストのフィールド名

`name=""`に書かれている部分のこと。

`<input name="email">`ならemailが入る。

### $value => フォーム内の値

emailのフォームに書かれている値のこと。

`<input name="email">`にexample@gmail.comが入っていれば、$valueはexample@gmail.comになる。

### $parameter => バリデーションで指定した値

先ほどのリクエストのコードで値を指定した時の値になる。

```
public function rules()
    {
        return [
            'email' => 'required|email|foo: 100, 200',
        ];
    }
```
100と200が指定されているので、`$parameter = [100, 200]`のように配列で取得できる。

### $validator => バリデーション名

第一引数で指定した、ここだと`foo`が入る。

この4つの引数を使って独自のバリデーションを作成することができる。

## replacerメソッド

エラーメッセージについても編集が必要になるだろう。

そんな時は`replacer`を使うことで解決することができる。

```
//  $parameterは上で書いたものを使用します。$parameter = [100, 200]
\Validator::replacer('message_max', function ($message, $attribute, $rule, $parameters) {
          return str_replace([':max'], 200, $message);
 });
```

これらを1つずつ解説していく。

### $message => エラーメッセージ

エラーになった時のメッセージ。

ここが今回の修正ポイント。

### $attribute => エラーが発生したキー名

先ほどの`email`でエラーが発生したなら$attributeは`email`になる。

### $rule => 引っかかったバリデーションルール

`email`が`required`で引っかかったら、`required`になる

### $parameters => バリデーションで指定している値

今回の場合は、[100]とする。

上記を踏まえると、

$messageの:maxという部分を$parameter(100)に変更する。

この:maxがどこから出てきたかというと、Requestファイルに以下のようにメッセージが書き込んである前提で進めると、

```
public function messages()
    {
        return [
            'email.foo' => __('e.max'),
        ];
    }
```

この` __('e.max')`は、「:max文字以内で入力してください」というエラーメッセージになる。

クロージャ内の` return str_replace([':max'], '3行’, $message);`は、$messageの:maxを200という文字に変更するという内容だから、「200文字以内で入力してください」となる。

つまりこの一連のバリデーションは、**100文字以内で入力してもらうが、エラーメッセージは200文字以内で入力せよ**というよくわからないバリデーションルールができあがるわけである。

これは全く意味のない例だが、この書き方を参考に独自のルールを作ることができるはずだ。

最後に全体のコードを掲載しておく。

```
Validator::extend('foo', function ($attribute, $value, $parameters, $validator) {
            return $value <= $parameters;
 });

\Validator::replacer('message_max', function ($message, $attribute, $rule, $parameters) {
          return str_replace([':max'], 200, $message);
 });
```

```
public function rules()
    {
        return [
            'email' => 'required|email|foo: 100',
        ];
    }

public function messages()
    {
        return [
            'email.foo' => __('e.max'),
        ];
    }
```
