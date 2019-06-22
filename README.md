# dont-use-repro-like-this

## Repro Web を導入する
- Repro に [Sign Up](https://app.repro.io/suppliers/sign_up) する
- アプリ設定を開くと SDK トークンが書いてある

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/01.png)

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/02.png)

- `index.html` に計測タグ設置 ([参考](https://docs.repro.io/ja/dev/web/getstarted/web.html))

```sh
<script>
    !function(o,e,n){var r=[];window.reproio=function(){r.push(arguments)};var i=o.createElement(e),t=o.getElementsByTagName(e)[0];i.src="https://cdn.reproio.com/web/v2/repro-sdk.min.js",i.async=!0,i.crossOrigin="",i.onload=function(){window.reproio("setSnippetVersion","2.0"),r.forEach(function(o){window.reproio.apply(window.reproio,o)})},t.parentNode.insertBefore(i,t)}(document,"script");
    reproio("setup", "YOUR_REPRO_SDK_TOKEN");
</script>
```

## 確認する
とりあえず [serve](https://github.com/zeit/serve) とかでサーブ

```sh
$ serve --single .

   ┌────────────────────────────────────────────────────┐
   │                                                    │
   │   Serving!                                         │
   │                                                    │
   │   - Local:            http://localhost:5000        │
   │   - On Your Network:  http://192.168.108.69:5000   │
   │                                                    │
   │   Copied local address to clipboard!               │
   │                                                    │
   └────────────────────────────────────────────────────┘
```

この時点ではもちろん真っ白画面


## マーケティングメッセージ機能に着目する

マーケティングツールになじみのないエンジニアにとって Repro の機能と使い方を理解する気は起きないですよね？  
でも大丈夫！たった１機能、しかもマーケティングに何も関係なく使います！

マーケティングのメッセージという機能があります。

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/10.png)

これ使うと、いろんな種類のテンプレートから選んで画面上にメッセージを表示できます

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/11.png)

この作成画面を開くと、キャンペーンとか配信設定とか、いかにもマーケ用語がでてきてうわぁとなるかもしれませんが、  
それらを見ないようにして、`メッセージ`の部分だけみてください  
適当に見出しと本文とボタンラベルを設定して、`プレビューをサイトで確認`

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/12.png)

URLを設定してプレビューしてみましょう

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/13.png)

すると、画面にメッセージが表示されますね

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/14.png)


今度は、`オーバーレイ`と`閉じるボタン`のチェックをはずし、  
見出しと本文とボタンラベルにこんなような内容を入れてプレビューしてみます  

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/20.png)

こんな感じ  

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/21.png)

これもう、立派なプロフィールサイトじゃないですか？

つまりReproは、  
見出し（タイトル）と本文とメニューを設定できる時点で、___もはやCMSということなのだ！___  
しかもPCとスマホ両対応でプレビュー付きという、とてもリッチな仕様！


## 画面遷移に対応する

さて、今のままだと、ブラウザでサイトを初めて開いた時に、特定の人に表示するようにしか設定できないので、  
ホーム画面を開けばホーム用メッセージ、プロフィール画面を開けばプロフィール用メッセージ、を常に表示するような設定をします。

### ~~全員に表示する事前準備~~
~~`全ユーザー`オーディエンスを作成しましょう~~ どうやら初回ユーザーは含まれていないそうです

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/30.png)

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/31.png)

### 各画面を表示する事前準備
`Web設定`のトラッキングルールを「ルーティング設定」と読みかえて、それぞれの画面URLにアクセスした際にイベントが発生するようにします

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/40.png)

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/41.png)

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/42.png)

一度イベントを発生させないと、メッセージトリガーに選択できないんで、イベント設定で全部のイベント登録されてるか確認します。

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/43.png)

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/44.png)

今 home しかないですね。  
一度サイトの /profile にアクセスして、もう一度みると、

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/45.png)

profileもでました。

イベント名付けておくと後々みやすいかもしれませんね

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/46.png)

### メッセージを設定する
では本番です。

キャンペーンは「ページ」と読みかえましょう。要はページタイトルを入力しましょう

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/50.png)

配信期間めちゃくちゃ長くしましょう

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/51.png)

何度でも表示しましょう

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/52.png)

ホーム用メッセージなら先ほど作成したホーム画面イベントをトリガーにしましょう

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/53.png)

全員を対象にしましょう

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/54.png)

メッセージ、もといページを公開したら、Webサイト作成完了です！

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/55.png)

#### ホーム画面
![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/60.png)

#### プロフィール画面
![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/61.png)


## デザインをカスタムする
ちなみに、ページのテンプレートだと、最大２ボタンまでしか用意されてないので、
２つの選択肢のみで全てのコンテンツを網羅したWebサイトをつくらなければいけない。

![Screen Shot](https://boiyaa.github.io/dont-use-repro-like-this/images/70.png)

もっとこだわった画面を作りたい人のために、[`カスタムメッセージ （ベータ版）`](https://docs.repro.io/ja/dashboard/campaign/custom-message.html) という機能があり、これを申し込みましょう。




いやー Repro 、非常に便利なCMSですね！
ヘッドレスCMSとか使ってる方々、乙でーすwwwww
