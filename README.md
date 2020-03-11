# mynews

PHP/Laravel 08～から始まるソース  
https://tech-boost.jp/common/books/326  


# PHP/Laravel 08 ControllerとRoutingの関係について理解しよう
課題

- `Controller`と`Routing`についての説明
    + アクセスしたときに、URLコマンドの処理を まず Routing に投げて振り分かる、 処理の方法を Controller 内にある Action 次第に処理を分けていく。
      + artisan を使って HogeController を作る。 HogeController の中に各種 Action(function) を作る。
        + 記事系なら、追加、作成、編集、アップロード みたいな内部機能を追加する。
- Controllerの役割について、説明してください。
    + 様々な function を 名称・種類別に保管するフォルダー
- ControllerとRoutingの役割について、説明してください。
    + Routing の処理が`routes/web.php`で定義されているんなら、 function追加次第、追記する必要があるんじゃない？
      https://www.wakuwakubank.com/posts/454-laravel-resourcefull-controller/
      https://www.ritolab.com/entry/119
    + ↑この辺にある変数を使っていったほうが保守し易いのでは？

# PHP/Laravel 09 Routingについて理解する  
課題

- URLとControllerやActionを紐付ける機能を何といいますか？
    + Routing？
- あなたが考える、group化をすることのメリットを考えてみてください。
    + まとまる → 見やすくなる → 保守しやすい → URL名の変更が 1箇所で済む  
- 「http://XXXXXX.jp/XXX というアクセスが来たときに、 AAAControllerのbbbというAction に渡すRoutingの設定」を書いてみてください。
    + `Route::get('XXX', 'XXX\AAAController@bbb');`
    + または

```php
    Route::group(['prefix'=>'XXX'],function() 
    {
      Route::get('/','XXX\AAAController@bbb');// '/' これを入れくるらいなら、グループ化しないほうがいいんじゃね？… 
    });
```

# PHP/Laravel 10 ControllerとViewが連携できるようにしよう	
課題
- Viewは何をするところでしょうか。簡潔に説明してみてください。
    + ユーザー固有のDBに合わせてhtmlを生成する所。
    + Controller から飛んできた指示にユーザー毎、ModelからDBを拾ってきた物をページ固有のテンプレに合わせてhtml生成している
- プログラマーがhtmlを書かずにPHPなどのプログラミング言語やフレームワークを使う必要があるのはどういった理由でしょうか。
    + htmlのテンプレとDBを用意し、ユーザ毎に違う表示にするため。
    + htmlを書いちゃうと、このメモのように、全部おんなじ表内容になってしまうから。

# PHP/Laravel 11 Bladeテンプレートの継承とLaravel Mixの使い方を活用してみよう	
課題
- Bladeテンプレートで、埋め込みたい箇所に利用するワードは何だったでしょうか？
    + `@yield @section`
- Webpackで使われているBootstrapやSCSSはどういったものか、調べられる範囲で調べてみましょう。
    + Bootstrap → 考えなくてもテンプレから作れるページデザイン作れる。CSSフレームワーク。ちょっと重めなのをよく聞く。
    + SCSS → ↓ の2個を見た感じ、コンパイルが必要だけど、**関数、変数**を使える、**演算、入れ子**可能、特に**継承**を使えるから、後からの手直しで感激するイメージを感じる
      [Sass（SCSS）でCSSコーディングを効率化・メリットと使い方を知る](https://tech.qookie.jp/posts/info-sass-scss-feature/)
      [プログラマーから見た、SCSSの正しい(かもしれない)使いかた](https://qiita.com/sasuraisan/items/9a9dfb281cfdf5a12bd3)


6. 【応用】 webpack.mix.jsを編集して、profile.scss をコンパイルするように編集してみましょう。
    + `webpack.mix.js`で `parsing error unexpected token`
    +  npm run watch を叩くと 案の定 `npm ERR! code ELIFECYCLE` ERROR
      [npm run watchエラーになった場合](https://qiita.com/ishizukih/items/9673e709832dacaa5155) ← node modules 再インスコも駄目
      + `webpack.mix.js`の書きミスだと判明。 JSでは末尾にセミコロン(;)なんだよ！
```php
  mix.js('resources/js/app.js', 'public/js')
     .sass('resources/sass/app.scss', 'public/css')
     .sass('resources/sass/admin.scss', 'public/css')「;」 ←こいつ
     .sass('resources/sass/profile.scss', 'public/css')（;） ← 本来はここにだけ付ける
```
        + いや普通文の終わりには;付けるでしょ(Java並感)
        + 尚、セミコロン付ける派、いらない派、returnで値を返すときは決して直後に改行を入れない理論。とか色々あるらしい。
          + [JavaScriptの行末セミコロンは省略すべきか](https://blog.tai2.net/automatic_semilocon_insertion.html)
          + セミコロンなくても動いたし、無い方がみんな幸せじゃん…？
      + `webpack.mix.js`直した結果、無事 `npm ERR! code ELIFECYCLE` ERROR喰らいました。(　 Д )　ﾟ　ﾟ
        + それこそnode modules 再インスコ で走って、バンザイ…

11:51 ちなみに…
  - Layouts(hoge.blade.php)が出来れば、継承先(@yield)の`views/admin/hoge/create.blade.php`にはHTMLタグとかいらないみたいです。
    + 書いとけし… 
