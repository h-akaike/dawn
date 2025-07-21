# Dawn プロジェクト構成

## 概要
DawnはShopifyテーマ開発のリファレンスプロジェクトです。以下にファイル構造の簡単な概要を説明します。

## ディレクトリ構造
- **assets/**: CSSスタイルシート、JavaScriptファイル、画像などの静的アセット
- **config/**: テーマ設定ファイル（例: settings_schema.json）
- **layout/**: ベースレイアウトファイル（例: theme.liquid）
- **locales/**: 多言語翻訳ファイル（JSON形式）
- **sections/**: 再利用可能なセクション（例: header-section.liquid）
- **snippets/**: 小さな再利用可能なコードスニペット（例: icon-snippet.liquid）
- **templates/**: ページテンプレート（例: index.liquid、product.liquid）

## その他のファイル
- **README.md**: プロジェクト概要と開始方法（日本語版）
- **.github/**: GitHub関連ファイル（CONTRIBUTING.mdなど）
- **.gitignore**: Git除外設定
- **.prettierrc.json**: コードフォーマッター設定
- **.theme-check.yml**: テーマチェック設定
- **LICENSE.md**: ライセンス情報

## クラス構成

### CSSクラス構成
Dawnは**BEM（Block Element Modifier）**メソドロジーに基づいたCSSクラス命名規則を使用しています：

#### **基本クラス**
- **`.page-width`**: ページ幅の制御
- **`.grid`**: グリッドレイアウト
- **`.button`**: ボタンスタイル
- **`.card`**: カードコンポーネント
- **`.media`**: メディア要素

#### **コンポーネントクラス**
- **`.product-card-wrapper`**: 商品カード
- **`.collection-card-wrapper`**: コレクションカード
- **`.article-card-wrapper`**: 記事カード
- **`.header__icon`**: ヘッダーアイコン
- **`.search-modal`**: 検索モーダル

#### **ユーティリティクラス**
- **`.hidden`**: 非表示
- **`.visually-hidden`**: 視覚的に非表示
- **`.center`**: 中央揃え
- **`.uppercase`**: 大文字変換

### JavaScriptクラス構成
Dawnは**Web Components**と**ES6クラス**を使用したモダンなJavaScript構成：

#### **コアユーティリティクラス**
- **`SectionId`**: セクションID管理
- **`HTMLUpdateUtility`**: HTML更新ユーティリティ
- **`CartPerformance`**: カートパフォーマンス測定

#### **UIコンポーネントクラス**
- **`MenuDrawer`**: メニュードロワー
- **`HeaderDrawer`**: ヘッダードロワー
- **`ModalDialog`**: モーダルダイアログ
- **`SliderComponent`**: スライダー
- **`SlideshowComponent`**: スライドショー

#### **機能クラス**
- **`QuantityInput`**: 数量入力
- **`VariantSelects`**: バリエーション選択
- **`ProductRecommendations`**: 商品推薦
- **`BulkAdd`**: 一括追加

### ファイル構成パターン
```
assets/
├── base.css              # 基本スタイル
├── global.js             # グローバルJavaScript
├── component-*.css       # コンポーネント別CSS
├── section-*.css         # セクション別CSS
├── template-*.css        # テンプレート別CSS
└── *.js                  # 機能別JavaScript
```

## 簡単な扱い方

### 1. 開発環境のセットアップ
```bash
# Shopify CLIをインストール（まだの場合）
npm install -g @shopify/cli @shopify/theme

# 開発サーバーを起動
shopify theme serve
```

### 2. 基本的なカスタマイズ
- **ヘッダー変更**: `sections/header.liquid`を編集
- **フッター変更**: `sections/footer.liquid`を編集
- **スタイル変更**: `assets/base.css`を編集
- **色やフォント**: `config/settings_schema.json`で設定

### 3. よく使うコマンド
```bash
# 開発サーバー起動
shopify theme serve

# テーマチェック実行
shopify theme check

# 本番環境にデプロイ
shopify theme push

# 本番環境からダウンロード
shopify theme pull
```

### 4. ファイル編集のコツ
- **Liquid構文**: `{{ }}`で変数、`{% %}`でロジック
- **セクション**: ページの大きなブロック（例: 商品一覧）
- **スニペット**: 小さな再利用可能なパーツ（例: ボタン）
- **アセット**: CSS/JSファイルは`assets/`に配置

### 5. デバッグ方法
- ブラウザの開発者ツールでHTML/CSS確認
- Shopify CLIのログでエラー確認
- `console.log()`でJavaScriptデバッグ

## 開発のヒント
- Shopify CLIを使って`shopify theme serve`でローカルサーバーを起動
- 詳細はShopify.devの[テーマ開発ドキュメント](https://shopify.dev/themes)を参照

この構造は標準的なShopifyテーマに基づいています。カスタマイズはsections/やsnippets/から始めましょう！ 