---
title: 静的ジェネレータでブログを書く3つのメリット
date: "2019-01-29T12:00:00.169Z"
layout: post
draft: false
path: "/posts/recommended-static-page/"
category: "Web Development"
tags:
  - "Web Development"
description: "このブログは静的ジェネレータで運営しています。ということで、静的ジェネレータを使うメリットをまとめる。"
---

静的ジェネレータとは、データベースを使わずサーバサイドの言語も使わない1枚のページから成る静的ページをWEB上に公開するものである。

簡単な例だと、HTMLファイルがそれに当たる。

```
<html>
    <h1>Helloworld</h1>
    <p>Helloworld</p>
</html>
```

このようなHTML言語で書かれたページをWEBに公開すると、Helloworldという文字が2行並ぶ。

これが静的なページである。再現が難しいが、動的なサイトの例も上げてみる。

```
<html>
    <h1><?php $title ?></h1> 
    <p><?php $text ?></p>
</html>
```

これはPHPという言語を使ってデータベースから値を取り出している。

`$title`という変数に`hello`という文字が入っていればHelloと表示される。

ほとんどのブログやWEBサービスではこの**動的サイト**を使っているが、静的サイトのメリットもあるので紹介する。

## とにかく早い

動的サイトの場合、データベースに値を取りに行く（リクエスト）、値が返ってくる（レスポンス）という動作の後にブラウザに表示される。

その分タイムロスが生まれるわけだが、静的サイトは書いてある文字をそのまま表示するのでデータベースとの通信分早くなる。

WEBページがサクサク動くように感じるので非常に使いやすいサイトになる。

## データの保管が簡単

動的サイトの場合データの保管方法は基本的にサーバをレンタルしてそのデータベース内にデータを置いておく。

もちろん定期的にバックアップをすることができるが、このバックアップの手間がある。

対して静的サイトは自分のPC内にすべてのデータがあって、そのコピーをサーバにアップするので、データは常に手元にある。

レンタルサーバであればバックアップが取れるが、もしサーバ会社が潰れてしまうとデータもなくなってしまう。

動的サイトであってもデータは自分の手元で管理できるようにするべき。

## 技術力を高めることができる

この静的サイトの技術と動的サイトの技術を合わせて、データを取得しつつも1つのページでサクサク動かすというシングルページアプリケーション（SPA）が流行っている。

この流れに乗るとすると、静的サイト向けのJavascriptという言語スキルの習得が不可欠になってくる。

JavaScriptを学ぶことができるという点に関しても、この静的サイトを運営するメリットはあるだろう。

ちなみにこのJavaScriptはフロントエンドエンジニアの言語であるが、サーバサイドエンジニアやデザイナーも習得すると武器になるスキルなので、ぜひ習得してほしい。

## まとめ

ページ内に動きをつけるのが流行りだし、ページをいちいち切り替えるのが面倒くさいというニーズもあり、この静的サイトはこれから需要が高まるはずである。

ブログの王様であるWordpressは動的サイトであり、かなり使いやすいのは間違いないが、フロントエンドエンジニアであるなら、ぜひこの静的サイトを運営すべきである。

あとは、Wordpresssっぽいブログが蔓延している中で一味違うブログを作るかっこよさも感じるから、私は静的サイトで運営している部分もある。