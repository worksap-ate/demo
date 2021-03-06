# Web UI ライブラリ 比較表

以下の3つのJavaScript Web UI ライブラリの機能について調査。

- [ExtJS](http://www.sencha.com/products/extjs/)
- [SmartClient](http://www.smartclient.com/)
- [qooxdoo](http://qooxdoo.org/)


## 概要

各種ライブラリの概要は以下の通り。

          項目            |          ExtJS             |          SmartClient       |          qooxdoo
 ------------------------ | -------------------------- | -------------------------- | --------------------------
 現行バージョン(2013/7/9) | 4.2.1                      | 9.0                        | 2.1.1
 ライセンス               | GPLv3/ExtJS商用ライセンス  | LGPL                       | LGPL/EPL
 商用利用                 |開発者毎にライセンス料が発生| 可                         | 可
 言語                     | JavaScript                 | JavaScript                 | JavaScript
 デバッグ/リリース版*1    | あり*2                     | なし                       | なし
 ビルドの必要性           | なし                       | なし                       | あり(Pythonが必要)


*1. デバッグ用のライブラリ(コンソールに情報が表示されたりするもの)とリリース用のライブラリで分かれているかどうか。

*2. bootstrap.jsを使ってライブラリを読み込むと、ホストがlocalhostの場合はデバッグ版に、それ以外の場合はリリース版に自動で切り替わる。デバッグ版にある機能がリリース版にはないということもある。



## フレームワークの機能

フレームワークが提供する機能(開発支援や、言語拡張的なものなど)の有無は以下。


 機能                     |      ExtJS                 |    SmartClient             |     qooxdoo
 ------------------------ | -------------------------- | -------------------------- | ----------------------
 デバッグコンソール       | ×                         | ○                         | ○
 テストフレームワーク     | ×(Jasmine推奨)            | ×(Selenium推奨)           | ○
 モジュール・依存関係制御*1 | ○                       | ×                         | △*2
 クラス*3                 | ○                         | ○ (通常は使わない)        | ○
 継承*3                   | ○                         | ○                         | ○
 mixin*3                  | ○                         | ×                         | ○
 多言語対応               | ○                         | ○                         | ○
 テーマ                   | 複数選択可(4種)            | 複数選択可(8種)            | 複数選択可(4種)
 カスタムテーマ           | ○                          | ○                          | ○
 Storeを経由した通信*4    | あり(経由しなくてもよい)   | あり(経由しなくてもよい)   | あり(経由しなくてもよい)


*1. 値や関数のまとまりに名前をつけることができ、それを外部から利用することができるかどうか。また、JavaScript側(HTMLではなく)で依存しているファイルを指定して読み込むことができるかどうか。

*2. 依存しているファイルを明示する機構はなく、暗黙的に依存しているファイルを読み込む。

*3. 言語ではなくフレームワークが提供するもの。

*4. Store(DataSourceとも)は"データが保存してある場所"を抽象化したもの。フレームワークの各コンポーネントが必ずこれを経由しなければいけない場合、柔軟性や他のライブラリとの適合性が低くなる。




## コンポーネント・レイアウトの有無


以下のコンポーネント・レイアウトについて調査。

 コンポーネント・レイアウト   |      説明                     |    例
 ---------------------------- | ----------------------------- | ---------------------------
 Grid                         | 一つのデータが行、そのフィールドが列になって、データのリストを表示できるコンポーネント | Wc3/EC2管理ページ/アマゾンマシンイメージ一覧
 GroupGrid                    | Gridに、データのあるフィールドに着目してグループ化する機能がついたもの | Wc3/レポートページ/AWS Health Status一覧
 TreeGrid                     | Gridにツリー(入れ子)で表示する機能がついたもの | Wc3/サーバ一覧ページ/サーバ一覧
 Paging                       | ページング処理ができるコンポーネント | Wc3/レポートページ/ログ一覧の下部
 Toolbar                      | ある操作を割り当てたアイコン付きのボタンなどが置かれるコンポーネント | Wc3/サーバ一覧ページ/サーバ一覧の上部にあるリフレッシュボタンなどがならんだもの
 ContextMenu                  | 右クリックで現れるメニュー及び右クリックによるイベントを操作できるかどうか | Wc3/アカウント管理ページにてグリッドを右クリックすることで現れるメニュー
 Form                         | 入力フォームのコンポーネント  | Wc3/サーバ一覧ページ/新しい構成
 BorderLayout                 | "north", "west", "east", "center", "south"などを指定してコンポーネントを配置するレイアウト | Wc3/サーバ一覧ページ(ページヘッダがnorth、サーバプロパティがeast、サーバ一覧がcenter)
 TableLayout                  | HTMLのテーブルのようにコンポーネントを配置するレイアウト | http://www.objis.com/formationextjs/lib/extjs-4.0.0/docs/api/Ext.layout.container.Table.html


以上のものがWeb UI ライブラリにデフォルトで存在していれば○、そうでなければ×とする。

 コンポーネント・レイアウト   |      ExtJS                    |    SmartClient              |     qooxdoo
 ---------------------------- | ----------------------------- | --------------------------- | --------------------------
 Grid                         | ○                            | ○                          | ○
 GroupGrid                    | ○                            | ○ *1                       | ×
 TreeGrid                     | ○                            | ○                          | △ *2
 paging                       | ○ *3                         | ×                          | ×
 toolbar                      | ○                            | ○                          | ○
 ContextMenu                  | ○                            | ○                          | ○
 Form                         | ○                            | ○*4                          | ○*5
 BorderLayout                 | ○                            | ×*6                        | ○*7
 TableLayout                  | ○                            | ○                          | ○


*1. グループでの総計表示機能あり(ExtJSにはない)。

*2. ツリーにはできるが、カラム名を表示できない。

*3. Store経由でなければならない(Storeについてはフレームワークの機能の*4を参照)。

*4. フィールドは連想配列(フィールド名、型)で指定。入力された値をgetするときはform.getValues、値をsetするときはform.setData。

*5. フィールドはフィールドオブジェクトのインスタンスをそれぞれ作り、Formオブジェクトに追加していく方式。getはform.createModel()から、setはform.createModel()で得たモデルにそれぞれの値をsetしていく。

*6. 直接的には存在しないが、VLayout(縦に並べるレイアウト)とHLayout(横に並べるレイアウト)を使えば同様のことは実現できる。

*7. Dockという名称で提供されている。



## 外部ライブラリやAltJSとの併用

 ライブラリ・AltJS       |       ExtJS                |    SmartClient              |     qooxdoo
 ----------------------- | -------------------------- | --------------------------- | --------------------------
 RequireJS               | 必要なし*1                 | ○*2                        | 必要なし*1
 bacon                   | ○                         | ○                          | ○
 jQuery                  | ○                         | ○                          | ○
 Haxe                    | ○*3                       | ○*4                       | ×*5


*1. 外部ライブラリが提供する機能がUIライブラリに既に実装されているため。

*2. SmartClientには独自のモジュール機構がないので、通常のJSファイルと同じようにRequireJSが使える。

*3. `extern class`を使って実装の本体をJS側にすればHaxeを使える。

*4. `var isc: ISC = untyped __js__('isc') // iscはSmartClientのオブジェクト` として型付けしていけばHaxeを使える。

*5. qooxdooはビルドが必要なので、qooxdooとHaxeを併用すると Haxe -> qooxdoo -> JavaScript と2段階のビルドが必要となるが、Haxeのビルドでqooxdooのビルドが通るようなJavaScriptを出力するのは難しいため。
