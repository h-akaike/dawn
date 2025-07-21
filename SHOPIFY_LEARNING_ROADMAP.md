# Shopify 体系的学習ロードマップ 🚀

## 概要

Shopifyの学習を段階的に進めるための完全ガイドです。初心者から上級者まで、効率的にスキルを身につけることができます。

## 📚 学習レベル別ロードマップ

### **Level 1: 基礎知識（1-2週間）**

#### **1.1 Shopifyの基本概念**
- [ ] **Shopifyとは何か**
  - ECプラットフォームとしての特徴
  - 他のプラットフォームとの違い
  - 料金プランと機能

- [ ] **Shopifyの基本用語**
  - 商品（Product）
  - コレクション（Collection）
  - テーマ（Theme）
  - アプリ（App）
  - セクション（Section）
  - ブロック（Block）

#### **1.2 管理画面の操作**
- [ ] **商品管理**
  - 商品の追加・編集・削除
  - バリエーションの設定
  - 在庫管理
  - 画像のアップロード

- [ ] **注文管理**
  - 注文の確認・処理
  - 配送設定
  - 返品・交換処理

- [ ] **顧客管理**
  - 顧客情報の確認
  - 顧客グループの作成
  - メール配信

#### **学習リソース**
```
📖 公式ドキュメント
- Shopify Help Center: https://help.shopify.com/
- Shopify 101: https://help.shopify.com/ja/manual/intro-to-shopify

🎥 動画学習
- Shopify公式YouTubeチャンネル
- Udemy: "Shopify for Beginners"

📱 実践
- 無料トライアルで実際に操作
- サンプル商品を追加してみる
```

---

### **Level 2: テーマ開発基礎（2-4週間）**

#### **2.1 Liquidテンプレート言語**
- [ ] **Liquidの基本構文**
  ```liquid
  {{ variable }}          # 変数出力
  {% if condition %}      # 条件分岐
  {% for item in items %} # ループ
  {% comment %}           # コメント
  ```

- [ ] **主要なLiquidオブジェクト**
  ```liquid
  {{ shop }}              # ショップ情報
  {{ product }}           # 商品情報
  {{ cart }}              # カート情報
  {{ customer }}          # 顧客情報
  {{ collection }}        # コレクション情報
  ```

- [ ] **フィルターの使用**
  ```liquid
  {{ product.price | money }}           # 通貨フォーマット
  {{ product.title | escape }}          # HTMLエスケープ
  {{ product.description | truncate: 100 }} # 文字数制限
  ```

#### **2.2 テーマ構造の理解**
- [ ] **ディレクトリ構造**
  ```
  themes/
  ├── assets/          # CSS, JS, 画像
  ├── config/          # 設定ファイル
  ├── layout/          # レイアウトテンプレート
  ├── sections/        # セクションファイル
  ├── snippets/        # 再利用可能なコード
  └── templates/       # ページテンプレート
  ```

- [ ] **テンプレートの種類**
  - `index.liquid` - ホームページ
  - `product.liquid` - 商品ページ
  - `collection.liquid` - コレクションページ
  - `cart.liquid` - カートページ
  - `page.liquid` - カスタムページ

#### **学習リソース**
```
📖 公式ドキュメント
- Liquid Reference: https://shopify.dev/docs/api/liquid
- Theme Development: https://shopify.dev/docs/themes

🎥 動画学習
- Shopify Dev YouTube: Liquid Tutorials
- Treehouse: "Shopify Theme Development"

💻 実践
- Dawnテーマをローカルで動かす
- 簡単なカスタマイズを試す
```

---

### **Level 3: テーマ開発応用（4-8週間）**

#### **3.1 Online Store 2.0**
- [ ] **セクションとブロック**
  ```json
  {
    "name": "商品情報",
    "settings": [
      {
        "type": "checkbox",
        "id": "show_price",
        "label": "価格を表示",
        "default": true
      }
    ],
    "blocks": [
      {
        "type": "text",
        "name": "テキスト",
        "settings": [
          {
            "type": "text",
            "id": "heading",
            "label": "見出し"
          }
        ]
      }
    ]
  }
  ```

- [ ] **JSONテンプレート**
  - ページレイアウトの定義
  - セクションの配置
  - ブロックの設定

- [ ] **アプリブロック**
  - アプリとの連携
  - カスタムアプリブロックの作成

#### **3.2 レスポンシブデザイン**
- [ ] **CSS Grid & Flexbox**
  ```css
  .product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
  }
  ```

- [ ] **メディアクエリ**
  ```css
  @media screen and (max-width: 768px) {
    .product-grid {
      grid-template-columns: 1fr;
    }
  }
  ```

#### **3.3 JavaScript統合**
- [ ] **Web Components**
  ```javascript
  class ProductForm extends HTMLElement {
    constructor() {
      super();
      this.addEventListener('submit', this.onSubmit.bind(this));
    }
    
    onSubmit(event) {
      // カスタム処理
    }
  }
  
  customElements.define('product-form', ProductForm);
  ```

#### **学習リソース**
```
📖 公式ドキュメント
- Online Store 2.0: https://shopify.dev/docs/themes/architecture/sections
- Theme Kit: https://shopify.dev/docs/themes/tools/theme-kit

🎥 動画学習
- Shopify Dev: "Building Sections"
- YouTube: "Shopify 2.0 Tutorials"

💻 実践
- カスタムセクションを作成
- レスポンシブデザインを実装
- JavaScript機能を追加
```

---

### **Level 4: アプリ開発（8-16週間）**

#### **4.1 Shopify App基礎**
- [ ] **アプリの種類**
  - Public App（App Store公開）
  - Private App（特定ショップ用）
  - Custom App（カスタム開発）

- [ ] **認証とセキュリティ**
  ```javascript
  // OAuth認証
  const shopify = new Shopify({
    shopName: 'your-shop.myshopify.com',
    accessToken: 'your-access-token'
  });
  ```

#### **4.2 APIの使用**
- [ ] **REST API**
  ```javascript
  // 商品一覧取得
  const products = await shopify.product.list();
  
  // 商品作成
  const newProduct = await shopify.product.create({
    title: 'New Product',
    body_html: '<p>Product description</p>',
    vendor: 'My Brand',
    product_type: 'Accessories'
  });
  ```

- [ ] **GraphQL API**
  ```javascript
  const query = `
    query {
      products(first: 10) {
        edges {
          node {
            id
            title
            handle
            priceRangeV2 {
              minVariantPrice {
                amount
                currencyCode
              }
            }
          }
        }
      }
    }
  `;
  
  const response = await shopify.graphql(query);
  ```

#### **4.3 Webhook**
- [ ] **イベント処理**
  ```javascript
  app.post('/webhooks/orders/create', async (req, res) => {
    const order = req.body;
    
    // 注文作成時の処理
    await processNewOrder(order);
    
    res.status(200).send();
  });
  ```

#### **学習リソース**
```
📖 公式ドキュメント
- App Development: https://shopify.dev/docs/apps
- API Reference: https://shopify.dev/docs/api
- GraphQL: https://shopify.dev/docs/api/graphql

🎥 動画学習
- Shopify Dev: "App Development Tutorials"
- YouTube: "Shopify App Development"

💻 実践
- 簡単なアプリを作成
- APIを使用してデータ取得
- Webhookを実装
```

---

### **Level 5: 高度な開発（16週間以降）**

#### **5.1 Shopify Functions**
- [ ] **サーバーレス関数**
  ```javascript
  export function run(input) {
    const { cart } = input;
    
    // カスタム割引ロジック
    const discount = calculateDiscount(cart);
    
    return {
      discountApplications: [{
        targetType: "ENTIRE_ORDER",
        type: "PERCENTAGE",
        value: discount
      }]
    };
  }
  ```

#### **5.2 Shopify Extensions**
- [ ] **管理画面拡張**
  ```javascript
  import { extend } from '@shopify/admin-ui-extensions';
  
  extend('Admin::Product::SubscriptionPlan::Create', (root, api) => {
    const customComponent = root.createComponent('div', {
      children: ['カスタム機能']
    });
    
    root.appendChild(customComponent);
  });
  ```

#### **5.3 パフォーマンス最適化**
- [ ] **画像最適化**
  ```liquid
  {{ product.image | image_url: width: 600, format: 'webp' }}
  ```

- [ ] **キャッシュ戦略**
  ```liquid
  {% cache 'product-card', product.id, product.updated_at %}
    <!-- 商品カードの内容 -->
  {% endcache %}
  ```

#### **学習リソース**
```
📖 公式ドキュメント
- Shopify Functions: https://shopify.dev/docs/apps/functions
- Extensions: https://shopify.dev/docs/apps/extensions
- Performance: https://shopify.dev/docs/themes/best-practices/performance

🎥 動画学習
- Shopify Dev: "Advanced Development"
- Conference Talks

💻 実践
- 複雑なアプリを開発
- パフォーマンステスト
- セキュリティ監査
```

---

## 🛠️ 開発環境セットアップ

### **必須ツール**
```bash
# 1. Node.js インストール
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 16
nvm use 16

# 2. Shopify CLI インストール
npm install -g @shopify/cli @shopify/theme

# 3. Git セットアップ
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 4. テーマ開発環境
shopify theme init my-theme
cd my-theme
shopify theme dev
```

### **推奨エディタ**
```
VS Code + 拡張機能:
- Shopify Liquid
- Shopify Theme Kit
- Prettier
- ESLint
- GitLens
```

---

## 📋 学習チェックリスト

### **基礎レベル**
- [ ] Shopify管理画面の操作に慣れる
- [ ] 基本的な商品・注文管理ができる
- [ ] Liquidの基本構文を理解する
- [ ] 簡単なテーマカスタマイズができる

### **中級レベル**
- [ ] カスタムセクションを作成できる
- [ ] レスポンシブデザインを実装できる
- [ ] JavaScript機能を追加できる
- [ ] 基本的なアプリ開発ができる

### **上級レベル**
- [ ] 複雑なビジネスロジックを実装できる
- [ ] パフォーマンス最適化ができる
- [ ] セキュリティを考慮した開発ができる
- [ ] チーム開発をリードできる

---

## 🎯 学習のコツ

### **1. 段階的に学習**
```
基礎 → 応用 → 実践 → 高度な技術
```

### **2. 実践重視**
```
- 実際に手を動かす
- サンプルプロジェクトを作る
- エラーを経験する
- デバッグを学ぶ
```

### **3. コミュニティ活用**
```
- Shopify Community Forum
- Stack Overflow
- GitHub
- Discord/Slack
```

### **4. 継続学習**
```
- 公式ブログを読む
- カンファレンスに参加
- 新しい機能を試す
- 他の開発者と交流
```

---

## 🚀 次のステップ

### **短期目標（3ヶ月）**
- [ ] 基本的なテーマ開発ができる
- [ ] 簡単なカスタマイズができる
- [ ] Liquidの基本をマスター

### **中期目標（6ヶ月）**
- [ ] カスタムセクションを作成
- [ ] 基本的なアプリ開発
- [ ] レスポンシブデザイン実装

### **長期目標（1年）**
- [ ] 複雑なアプリ開発
- [ ] パフォーマンス最適化
- [ ] チーム開発リード

---

## 📚 おすすめ学習リソース

### **公式リソース**
- [Shopify Dev](https://shopify.dev/) - 公式開発者ドキュメント
- [Shopify Help](https://help.shopify.com/) - ユーザー向けヘルプ
- [Shopify Blog](https://www.shopify.com/blog) - 公式ブログ

### **コミュニティ**
- [Shopify Community](https://community.shopify.com/) - 公式フォーラム
- [Stack Overflow](https://stackoverflow.com/questions/tagged/shopify) - Q&Aサイト
- [Reddit r/shopify](https://www.reddit.com/r/shopify/) - Redditコミュニティ

### **動画学習**
- [Shopify Dev YouTube](https://www.youtube.com/c/ShopifyDev) - 公式チャンネル
- [Udemy](https://www.udemy.com/topic/shopify/) - オンラインコース
- [Treehouse](https://teamtreehouse.com/library/shopify-theme-development) - プログラミング学習

### **書籍**
- "Shopify Theme Development" by Gavin Ballard
- "Liquid Template Language" by Shopify
- "Shopify App Development" by Shopify

---

## 🎉 まとめ

**Shopifyの学習は段階的に進めることが重要です：**

1. **✅ 基礎から始める** - 管理画面操作、基本概念
2. **✅ 実践重視** - 手を動かして学習
3. **✅ コミュニティ活用** - 他の開発者と交流
4. **✅ 継続学習** - 新しい技術を学び続ける

**このロードマップに従って学習すれば、効率的にShopify開発者として成長できます！** 🚀

何か質問があれば、いつでもお気軽にお聞きください！ 