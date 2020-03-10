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

