# Shopify Liquid オブジェクトとモデル開発ガイド

## 概要

Shopifyのテーマ開発では、**バックエンドのモデルは事前に定義されており**、Liquidテンプレート内で直接アクセスできます。従来のWeb開発とは異なり、データベーススキーマを自分で設計する必要はありません。

## 1. Shopifyのデータモデル構造

### **主要なLiquidオブジェクト**

#### **🔹 グローバルオブジェクト**
```liquid
{{ shop }}              # ショップ情報
{{ request }}           # リクエスト情報
{{ customer }}          # 現在の顧客
{{ cart }}              # カート情報
{{ settings }}          # テーマ設定
{{ localization }}      # 多言語・多通貨設定
```

#### **🔹 ページ固有オブジェクト**
```liquid
{{ product }}           # 商品情報（商品ページ）
{{ collection }}        # コレクション情報（コレクションページ）
{{ article }}           # 記事情報（ブログ記事ページ）
{{ page }}              # ページ情報（カスタムページ）
{{ blog }}              # ブログ情報（ブログページ）
```

#### **🔹 セクション・ブロックオブジェクト**
```liquid
{{ section }}           # セクション情報
{{ section.settings }}  # セクション設定
{{ section.blocks }}    # セクションブロック
{{ block }}             # 現在のブロック
{{ block.settings }}    # ブロック設定
```

## 2. 開発の進め方

### **Step 1: オブジェクトの構造を理解する**

#### **商品オブジェクト（product）の例**
```liquid
{{ product.id }}                    # 商品ID
{{ product.title }}                 # 商品タイトル
{{ product.description }}           # 商品説明
{{ product.price }}                 # 基本価格
{{ product.price_min }}             # 最低価格
{{ product.price_max }}             # 最高価格
{{ product.available }}             # 在庫状況
{{ product.featured_image }}        # メイン画像
{{ product.images }}                # 全画像
{{ product.variants }}              # バリエーション
{{ product.options_with_values }}   # オプション
{{ product.tags }}                  # タグ
{{ product.type }}                  # 商品タイプ
{{ product.vendor }}                # ベンダー
{{ product.url }}                   # 商品URL
```

#### **カートオブジェクト（cart）の例**
```liquid
{{ cart.item_count }}               # 商品数
{{ cart.total_price }}              # 合計金額
{{ cart.items }}                    # カート内商品
{{ cart.currency.iso_code }}        # 通貨コード
{{ cart.taxes_included }}           # 税込み表示
{{ cart.duties_included }}          # 関税込み表示
```

### **Step 2: 実際のコードで確認**

#### **商品ページでの使用例**
```liquid
<!-- 商品タイトル -->
<h1>{{ product.title }}</h1>

<!-- 商品価格 -->
<p>{{ product.price | money }}</p>

<!-- 在庫状況 -->
{% if product.available %}
  <p>在庫あり</p>
{% else %}
  <p>売り切れ</p>
{% endif %}

<!-- 商品画像 -->
{% if product.featured_image %}
  <img src="{{ product.featured_image | image_url: width: 600 }}" 
       alt="{{ product.featured_image.alt | escape }}">
{% endif %}

<!-- バリエーション -->
{% for variant in product.variants %}
  <option value="{{ variant.id }}">{{ variant.title }}</option>
{% endfor %}
```

### **Step 3: フィルターを活用**

#### **価格フィルター**
```liquid
{{ product.price | money }}                    # ¥1,000
{{ product.price | money_with_currency }}      # ¥1,000 JPY
{{ product.price | money_without_currency }}   # 1,000
```

#### **画像フィルター**
```liquid
{{ product.image | image_url: width: 300 }}    # 幅300px
{{ product.image | image_url: height: 400 }}   # 高さ400px
{{ product.image | image_url: width: 300, height: 400 }} # 両方指定
```

#### **テキストフィルター**
```liquid
{{ product.title | escape }}                   # HTMLエスケープ
{{ product.description | truncate: 100 }}      # 100文字制限
{{ product.title | upcase }}                   # 大文字変換
{{ product.title | downcase }}                 # 小文字変換
```

## 3. 開発ツールとリソース

### **🔧 Shopify CLI**
```bash
# テーマの開発サーバー起動
shopify theme dev

# テーマの同期
shopify theme push
shopify theme pull
```

### **📚 公式ドキュメント**
- **Liquid Reference**: https://shopify.dev/docs/api/liquid
- **Theme Kit**: https://shopify.dev/docs/themes/tools/theme-kit
- **Online Store 2.0**: https://shopify.dev/docs/themes/architecture/sections

### **🔍 デバッグ方法**

#### **1. 変数の内容を確認**
```liquid
<!-- デバッグ出力 -->
<pre>{{ product | json }}</pre>

<!-- 特定のプロパティを確認 -->
<pre>{{ product.variants | json }}</pre>
```

#### **2. 条件分岐でテスト**
```liquid
{% if product.available %}
  <p>✅ 商品は利用可能</p>
{% else %}
  <p>❌ 商品は利用不可</p>
{% endif %}

{% if product.variants.size > 1 %}
  <p>✅ 複数バリエーションあり</p>
{% else %}
  <p>❌ 単一商品</p>
{% endif %}
```

## 4. 実際の開発フロー

### **Step 1: 要件分析**
```liquid
<!-- 何を表示したいか？ -->
- 商品名: {{ product.title }}
- 価格: {{ product.price | money }}
- 在庫: {{ product.available }}
```

### **Step 2: テンプレート作成**
```liquid
<!-- sections/product-info.liquid -->
<div class="product-info">
  <h1>{{ product.title }}</h1>
  <p class="price">{{ product.price | money }}</p>
  
  {% if product.available %}
    <button class="add-to-cart">カートに追加</button>
  {% else %}
    <p class="sold-out">売り切れ</p>
  {% endif %}
</div>
```

### **Step 3: 設定可能にする**
```liquid
<!-- schema.json -->
{
  "name": "商品情報",
  "settings": [
    {
      "type": "checkbox",
      "id": "show_price",
      "label": "価格を表示",
      "default": true
    },
    {
      "type": "checkbox", 
      "id": "show_vendor",
      "label": "ベンダーを表示",
      "default": false
    }
  ]
}

<!-- テンプレート内で使用 -->
{% if section.settings.show_price %}
  <p class="price">{{ product.price | money }}</p>
{% endif %}

{% if section.settings.show_vendor %}
  <p class="vendor">{{ product.vendor }}</p>
{% endif %}
```

## 5. よく使うオブジェクトとプロパティ

### **商品関連**
```liquid
# 基本情報
product.id, product.title, product.description
product.price, product.price_min, product.price_max
product.available, product.published_at

# 画像
product.featured_image, product.images
product.media (動画、3Dモデル含む)

# バリエーション
product.variants, product.options_with_values
product.selected_or_first_available_variant

# メタデータ
product.tags, product.type, product.vendor
product.metafields
```

### **コレクション関連**
```liquid
# 基本情報
collection.id, collection.title, collection.description
collection.image, collection.products

# ページネーション
collection.products_count, collection.all_products_count
paginate collection.products by 12
```

### **カート関連**
```liquid
# 基本情報
cart.item_count, cart.total_price
cart.items, cart.currency

# 税金・配送
cart.taxes_included, cart.duties_included
cart.requires_shipping
```

## 6. ベストプラクティス

### **✅ 良い例**
```liquid
<!-- 条件チェックを先に行う -->
{% if product.available %}
  <button class="add-to-cart">カートに追加</button>
{% else %}
  <p class="sold-out">売り切れ</p>
{% endif %}

<!-- フィルターを適切に使用 -->
<img src="{{ product.image | image_url: width: 600 }}" 
     alt="{{ product.image.alt | escape }}">

<!-- デフォルト値を設定 -->
{{ product.description | default: '説明がありません' }}
```

### **❌ 避けるべき例**
```liquid
<!-- 存在しないプロパティにアクセス -->
{{ product.non_existent_property }}

<!-- フィルターなしでHTML出力 -->
{{ product.description }}  <!-- XSSの危険性 -->

<!-- 条件チェックなし -->
{{ product.variants.first.price }}  <!-- バリエーションがない場合エラー -->
```

## まとめ

**Shopifyのテーマ開発では：**

1. **✅ バックエンドモデルは事前定義済み**
2. **✅ Liquidオブジェクトで直接アクセス**
3. **✅ データベース設計は不要**
4. **✅ 公式ドキュメントで構造確認**
5. **✅ フィルターと条件分岐を活用**

**開発の流れ：**
1. 要件を整理
2. 必要なオブジェクトを特定
3. テンプレートを作成
4. 設定可能な項目を追加
5. テストとデバッグ

これで、Shopifyの豊富なデータモデルを活用して効率的にテーマ開発を進めることができます！🚀 