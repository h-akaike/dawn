# Dawn

[![Build status](https://github.com/shopify/dawn/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/Shopify/dawn/actions/workflows/ci.yml?query=branch%3Amain)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?color=informational)](/.github/CONTRIBUTING.md)

[はじめに](#はじめに) |
[Dawnの変更に追従する](#dawnの変更に追従する) |
[開発者ツール](#開発者ツール) |
[コントリビューション](#コントリビューション) |
[行動規範](#行動規範) |
[テーマストア提出](#テーマストア提出) |
[ライセンス](#ライセンス)

DawnはHTML優先、JavaScriptは必要な時のみという approach を採用したテーマ開発を表現しています。これはShopifyの最初のソース公開テーマであり、パフォーマンス、柔軟性、および[Online Store 2.0機能](https://www.shopify.com/partners/blog/shopify-online-store)が組み込まれており、Shopifyテーマ構築のリファレンスとして機能します。

* **最も純粋な形でのWeb-native：** テーマは[evergreen web](https://www.w3.org/2001/tag/doc/evergreen-web/)上で動作します。私たちは最新のWebブラウザを最大限に活用し、古いブラウザに対してはpolyfillではなくプログレッシブエンハンスメントを通じてサポートを維持します。
* **軽量、高速、信頼性：** 機能とデザインは、この要件を満たすまでデフォルトで「いいえ」です。コードは品質に基づいて出荷されます。テーマは目的を持って構築されるべきです。Shopifyのすべての機能をサポートすべきではありません。
* **サーバーレンダリング：** HTMLはLiquidを使用してShopifyサーバーによってレンダリングされる必要があります。ビジネスロジックや翻訳、金額フォーマットなどのプラットフォームプリミティブはクライアント側に属しません。ページの一部の非同期・オンデマンドレンダリングは可能ですが、プログレッシブエンハンスメントとしてまれに使用します。
* **機能的で、ピクセルパーフェクトではない：** Webは各ページが各ブラウザエンジンによってピクセルパーフェクトにレンダリングされることを要求しません。セマンティックマークアップ、プログレッシブエンハンスメント、巧妙なデザインを使用して、ブラウザに関係なくテーマが機能し続けることを保証します。

テーマコード原則のより詳細なバージョンは[コントリビューションガイド](https://github.com/Shopify/dawn/blob/main/.github/CONTRIBUTING.md#theme-code-principles)で確認できます。

## はじめに
テーマ開発の出発点としてDawnを使用することをお勧めします。[Shopify.devで詳細を学ぶ](https://shopify.dev/themes/getting-started/create)。

> Shopify Theme Store用のテーマを構築している場合は、Dawnを出発点として使用できます。ただし、提出するテーマは[Dawnとは実質的に異なる](https://shopify.dev/themes/store/requirements#uniqueness)必要があり、マーチャントに付加価値を提供する必要があります。[Dawnの使用方法](https://shopify.dev/themes/tools/dawn#ways-to-use-dawn)について学んでください。

mainブランチには、まだリリースされていない機能のコードが含まれている可能性があることにご注意ください。Dawnの「安定」バージョンはテーマストアで入手できます。

## Dawnの変更に追従する

Dawnを基にした新しいテーマを構築しているが、最新の変更を取り込みたい場合は、このDawnリポジトリを指すリモート`upstream`を追加できます。

1. ローカルテーマフォルダに移動します。
2. リモートのリストを確認し、`origin`と`upstream`の両方があることを確認します：
```sh
git remote -v
```
3. `upstream`が表示されない場合は、ShopifyのDawnリポジトリを指すものを追加できます：
```sh
git remote add upstream https://github.com/Shopify/dawn.git
```
4. 最新のDawnの変更をリポジトリに取り込みます：
```sh
git fetch upstream
git pull upstream main
```

## 開発者ツール

Shopify Themesチームが開発中に使用する非常に便利なツールがいくつかあります。Dawnはすでにこれらのツールと連携するように設定されています。

### Shopify CLI

[Shopify CLI](https://github.com/Shopify/shopify-cli)はShopifyテーマをより速く構築するのに役立ち、ローカル開発ワークフローを自動化し強化するために使用されます。Shopifyテーマ開発用のコマンドスイート（Shopifyストアでのテーマ操作（テーマの作成、公開、削除など）からローカルテーマ開発用の開発サーバーの起動まで）が含まれています。

[テーマ開発者向けクイックスタートガイド](https://shopify.dev/docs/themes/tools/cli)に従って開始できます。

### Theme Check

Shopifyテーマを検証・リントする方法として[Theme Check](https://github.com/shopify/theme-check)の使用をお勧めします。

DawnのVS Code拡張機能リスト[VS Code extensions](/.vscode/extensions.json)にTheme Checkを追加したため、Visual Studio Codeをコードエディターとして使用している場合、DawnをフォークしてクローンしてからVS Codeを開くと、[Theme Check VS Code](https://marketplace.visualstudio.com/items?itemName=Shopify.theme-check-vscode)拡張機能のインストールを促されます。

以下のShopify CLIコマンドでターミナルからも実行できます：

```bash
shopify theme check
```

### 継続的インテグレーション

Dawnはテーマのクオリティを維持するために[GitHub Actions](https://github.com/features/actions)を使用しています。[これは出発点](https://github.com/Shopify/dawn/blob/main/.github/workflows/ci.yml)であり、より良いテーマを構築するために使用することをお勧めします。ぜひこれを基に構築してください！

#### Shopify/lighthouse-ci-action

私たちは高速なWebサイトが大好きです！そのため[Shopify/lighthouse-ci-action](https://github.com/Shopify/lighthouse-ci-action)を作成しました。これはストアのホーム、商品、コレクションページに対して一連の[Google Lighthouse](https://developers.google.com/web/tools/lighthouse)監査を実行し、追加されるコードが時間の経過とともにストアフロントのパフォーマンスを低下させないことを保証します。

#### Shopify/theme-check-action

Dawnは[Shopify/theme-check-action](https://github.com/Shopify/theme-check-action)を介して、すべてのコミットで[Theme Check](#Theme-Check)を実行します。

## コントリビューション

Dawnに貢献してすべての人のためにコマースをより良くしませんか？私たちはあなたの助けを歓迎します！私たちの[コントリビューションガイド](https://github.com/Shopify/dawn/blob/main/.github/CONTRIBUTING.md)を読んで、開発プロセス、バグ修正と改善の提案方法、Dawnのための構築方法について学んでください。

## 行動規範

コードやissueを通じて貢献したいすべての開発者は、まず私たちの[行動規範](https://github.com/Shopify/dawn/blob/main/.github/CODE_OF_CONDUCT.md)を読んでください。

## テーマストア提出

[Shopify Theme Store](https://themes.shopify.com/)は、Shopifyマーチャントがビジネスを紹介・サポートするために使用するテーマを見つける場所です。テーマパートナーとして、Shopify Theme Store向けのテーマを作成し、絶えず成長している起業家の国際的なオーディエンスにリーチできます。

[Shopify Theme Partner](https://themes.shopify.com/services/themes/guidelines)になり、Shopifyプラットフォーム用のテーマを構築することに興味がある場合は、[テーマストア要件](https://shopify.dev/themes/store/requirements)のリストに従うことを確認してください。

## ライセンス

Copyright (c) 2021-present Shopify Inc. 詳細については[LICENSE](/LICENSE.md)を参照してください。
