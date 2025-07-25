# コントリビューション

[コントリビュート前に](#コントリビュート前に) |
[スコープ](#スコープ) |
[テーマコードの原則](#テーマコードの原則) |
[コードのコントリビュート](#コードのコントリビュート) |
[バグの報告](#バグの報告) |
[レビュー](#レビュー)

このドキュメントをお読みいただきありがとうございます。より多くの開発者にこのテーマへ貢献していただきたいと思っています！次の100万人の起業家のために構築することに情熱を持っているなら、あなたは正しい場所にいます。

## コントリビュート前に

Dawnでバグに遭遇した場合や有用な機能を思いついた場合は、[新しいイシューを作成](https://github.com/Shopify/dawn/issues/new)してください。コードに取り掛かる前にイシューを作成することで、それについて議論し、テーマの方向性と一致するかどうかを判断できます。

小さなバグ修正やタイポの修正であっても、テーマに貢献したい場合は、お気軽にどうぞ。どんな助けも大歓迎です！また、貢献は必ずしもコード関連だけではありません。イシュー、プルリクエスト、ディスカッションなどの形での貢献もあります。

## スコープ

このGitHubリポジトリは、テーマ開発コミュニティがDawnに直接関連する問題について議論し解決するために存在します。一般的なテーマ開発の問題を議論する場所**ではなく**、Dawn以外の問題に関する助けを求める場所でもありません。

Shopifyテーマ開発は大きなトピックであり、助けを求める必要がある問題に遭遇するのは完全に正常です。実際、私たちはすでにテーマ開発のためのいくつかの知識とサポートプラットフォームを提供しています：

* [Shopify Development](https://shopify.dev/themes)
* [Shopify ヘルプセンター](https://help.shopify.com/themes)
* [Shopify フォーラム](https://ecommerce.shopify.com/forums)
* [Shopify エキスパート](https://experts.shopify.com/)

## テーマコードの原則

Dawnに貢献する前に、テーマ開発に対する私たちの基本的なアプローチをよりよく理解するために、以下のテーマコードの原則をお読みください。Dawnのために構築する際は、これらの原則に従うことが期待されています。

### なぜこれらの原則なのか？

ブラウザは多くの問題を解決するためのAPIを提供しています：[WebGL](https://en.wikipedia.org/wiki/WebGL)や[WASM](https://en.wikipedia.org/wiki/WebAssembly)を搭載したアプリから静的なウェブサイトまで。使用する最適なAPIは、構築しているものによって異なります。テーマはeコマースウェブサイトを動かします。ほとんどの場合、_Webネイティブ_—ブラウザの組み込み機能を最大限に活用すること：HTTP、HTML、CSS、JavaScript、そしてDOM—はeコマースウェブサイトに完璧に適合します。eコマースには、主に「ログアウト」したトラフィックのために、信じられないほど高速なウェブサイトが必要です。

### 最も純粋な形でのWebネイティブ

_最も重要な原則。_

テーマは[エバーグリーンWeb](https://www.w3.org/2001/tag/doc/evergreen-web/)上で動作します。私たちは最新のWebブラウザを最大限に活用しながら、ポリフィルではなくプログレッシブエンハンスメントを通じて古いブラウザのサポートを維持します。

私たちは抽象化なしに、オーダーメイドのWebネイティブコードを書きます。フレームワーク、ライブラリ、依存関係は私たちのテーマには属しません。

私たちは、Webネイティブなeコマースをできるだけ良いものにするために、マーチャントに代わってブラウザエコシステムに関与します。

「繰り返さない」はアンチパターンです。私たちは少ないもので多くのことを行うよう最善を尽くしますが、繰り返しの周りに抽象化を構築しません。代わりに、一貫して良い最新のWebネイティブコードを強制するためにリンティングとテストを使用します。

### リーン、高速、信頼性

_原則的な要件。_

コードはリーン、高速、信頼性がなければなりません。私たちの目標には以下が含まれます：

* ゼロ[累積レイアウトシフト](https://web.dev/cls/)
* ユーザー入力前のDOM操作なし
* レンダリングをブロックするJavaScriptなし
* [長いタスク](https://developer.mozilla.org/en-US/docs/Web/API/Long_Tasks_API)なし

機能とデザインは、この要件を満たすまでデフォルトで「いいえ」です。コードは品質に基づいて出荷されます。

私たちは、Webネイティブであるという制約の中で、コードを容赦なく継続的に最適化します。ブラウザがまだ高速化していない機能がある場合、それを使用しないか、十分に高速であれば「そのまま」使用します。私たちは、ブラウザが時間とともに高速になることを信頼しています。

テーマは目的を持って構築されなければなりません。Shopifyのすべての機能をサポートする必要はありません。

### サーバーレンダリング

_私たちの主な制約。_

HTMLは[Liquid](https://shopify.dev/api/liquid)を使用してShopifyサーバーによってレンダリングされなければなりません。ビジネスロジックや翻訳、通貨フォーマットなどのプラットフォームプリミティブはクライアントに属しません。

サーバーレンダリングは「フルページリロード」を意味しません。ページの一部の非同期およびオンデマンドレンダリングはOKですが、プログレッシブエンハンスメントとして控えめに行います。

### 機能的、ピクセルパーフェクトではない

_購入者は誰も取り残されない。_

Webは、各ブラウザエンジンによって各ページがピクセルパーフェクトにレンダリングされることを要求しません。セマンティックマークアップ、プログレッシブエンハンスメント、賢いデザインを使用して、ブラウザに関係なくテーマが機能的であることを保証します。

そして、レガシーブラウザはしばしば最も遅いので、ポリフィルで負担をかけません。代わりに、Webのフェイルオープンな性質に頼って、「最小限だが機能的な」体験を提供します。

## コードのコントリビュート

ストアのセットアップからDawnのプルリクエスト作成まで、以下の手順に従うことができます。

>:information_source: GitとGitHubにすでに慣れていることを前提としています（これらに慣れていない場合は、[これらのドキュメントから始めてください](https://docs.github.com/github/getting-started-with-github/quickstart/set-up-git)）。

1. コードの変更をテストできるように[開発ストア](https://shopify.dev/themes/tools/development-stores)をセットアップします（すでにストアを持っていない場合）。
2. [これらの手順](https://shopify.dev/themes/tools/cli/installation)に従って[Shopify CLI](https://github.com/Shopify/shopify-cli)をインストールします。
3. リポジトリをフォークし、クローンして新しいブランチを作成します：
```sh
git clone git@github.com:your-username/dawn.git
cd dawn
git checkout -b your-new-branch-name
```
4. 開発サーバーを起動します：
```sh
shopify theme serve
```
5. コードベースに変更を加えます。
6. 変更をコミットします：
```sh
git commit -a -m="Your commit message"
```
7. フォークしたリポジトリにコミットをプッシュします：
```sh
git push origin your-new-branch-name
```
8. プルリクエストを開きます。詳細については、[GitHubの公式ドキュメント](https://help.github.com/articles/creating-a-pull-request-from-a-fork/)を参照してください。
9. プルリクエストをマージする前に、Shopifyの[コントリビューターライセンス契約（CLA）](https://cla.shopify.com/)に署名する必要があります。

## バグの報告

バグは[GitHubイシュー](https://github.com/Shopify/dawn/issues)として追跡されます。同様のバグが報告されているかどうかを確認するために、オープンイシューを検索してください。新しいものである場合は、[イシューを開いてください](https://github.com/Shopify/dawn/issues/new)。修正したい問題について会話するためにイシューを使用します。

新しいイシューを作成する際は、イシューが明確であり、メンテナーが再現するのに役立つ追加の詳細を含めてください：

* **問題を特定するために明確で説明的なタイトルを使用**してください。
* **問題を再現する正確な手順をできるだけ詳細に説明**してください。
* **手順を示す具体的な例を提供**してください。ファイルへのリンクや、コピー/ペースト可能なスニペットを含めてください。イシューでスニペットを提供する場合は、Markdownコードブロックを使用してください。
* **手順に従った後に観察した動作を説明**し、その動作の何が問題なのかを正確に指摘してください。
* **代わりに期待した動作とその理由を説明**してください。
* **可能な場合はスクリーンショットとアニメーションGIFを含めて**ください。

## レビュー

私たち（テーマチーム）はすべてのPRをレビューします。レビューの目的は、マーチャント、開発者、およびそれを使用する他の人々のために、Dawnの最高のバージョンを作成することです。

:yellow_heart: レビューは常に敬意を持って行われ、誰もがその時点で持っていた知識で最善の仕事をしたことを認めます。
:yellow_heart: レビューは、それを作成した人ではなく、コンテンツについて議論します。
:yellow_heart: レビューは建設的で、フィードバックについて会話を始めます。

### セルフレビュー

常に最初に自分のPRをレビューする必要があります。

コードの変更については、以下を確認してください：
- [ ] 変更が私たちの[テーマコードの原則](#テーマコードの原則)を満たしていることを確認します。
- [ ] 使用されているコードが最新であり、非推奨ではないことを確認するために、新しいまたは更新されたLiquidドキュメントを確認します。
- [ ] PRに失敗しているチェックがある場合は、すべて合格するまでトラブルシューティングします。
- [ ] @Shopify/themes-front-end-developersをレビュアーとして追加します。

### プルリクエストテンプレート

プルリクエストを開くときは、PRをレビューする前に「Ready for review」テンプレートに記入する必要があります。このテンプレートは、レビュアーがあなたの変更とプルリクエストの目的を理解するのに役立ちます。

### 提案された変更

PRがマージされる前に、[提案された変更](https://docs.github.com/github/collaborating-with-issues-and-pull-requests/incorporating-feedback-in-your-pull-request)またはプルリクエストのコメントを使用して、変更を求める場合があります。提案された変更はUIから直接適用できます。他の変更はフォークで行い、ブランチにコミットできます。

PRを更新して変更を適用する際は、各会話を[解決済み](https://docs.github.com/github/collaborating-with-issues-and-pull-requests/commenting-on-a-pull-request#resolving-conversations)としてマークしてください。