# Japan Watch Market — Cross-Shop Price Comparison

**Compare used luxury watch prices across Japan's top watch retailers in a single dataset.**

Scrapes listings from **Jackroad (ジャックロード)** — Tokyo's leading pre-owned luxury watch dealer — and **Kitamura (キタムラ)** — Japan's largest camera chain with a 395+ used watch inventory (Rolex, Citizen, Seiko, Grand Seiko, etc.). Each item is tagged with its `source` and `shop` so you can compare prices for the same model across shops.

## Why this is useful

- **Cross-shop price comparison** — the same Rolex Explorer often differs by 5-15% between shops
- **Resale arbitrage** — find underpriced watches, sell at market rate
- **Price monitoring** — track market moves before buying/selling
- **Condition & rank tracking** — compare condition labels (新品/中古/ヴィンテージ) and ranks across shops

## Input

| Field | Type | Default | Description |
|---|---|---|---|
| `searchKeyword` | string | `ROLEX` | Brand/model keyword (required for Jackroad) |
| `maxItems` | integer | 100 | Max items to collect |
| `maxPages` | integer | 2 | Max pages per source |
| `sources` | string | `jackroad,kitamura` | Comma-separated source list |

## Output fields

| Field | Description |
|---|---|
| `productId` | Product ID at source shop |
| `title` | Product title |
| `price` | Price in JPY |
| `brand` | Brand (ROLEX, OMEGA, SEIKO...) |
| `shop` | Source shop name |
| `category` | Category label |
| `condition` | Condition (新品/中古/ヴィンテージ, kitamura rank) |
| `stockStatus` | Jackroad stock status |
| `source` | `jackroad` or `kitamura` |
| `imageUrl` | Product image URL |
| `productUrl` | Product page URL |
| `scrapedAt` | Scrape timestamp |

## Output sample

```json
{
  "productId": "6341419",
  "title": "ロレックス エアキング",
  "price": 848000,
  "brand": "ロレックス",
  "condition": "ヴィンテージ",
  "stockStatus": "在庫あり",
  "productUrl": "https://www.jackroad.co.jp/shop/g/g6341419/",
  "imageUrl": "https://www.jackroad.co.jp/img/goods/S/6341419.jpg",
  "shop": "Jackroad",
  "source": "jackroad",
  "category": "中古時計",
  "scrapedAt": "2026-08-10T09:54:53.747321+00:00"
}
```

The `source` + `shop` fields let you compare the same watch model across shops: run once with `searchKeyword: "ROLEX"` and get Jackroad and Kitamura prices side by side.

## Pricing

Pay per event — $0.00005/run + **$0.002/item**.

## Data source notes

- **Jackroad**: server-side rendered search (30 items/page), brand extraction from title prefix.
- **Kitamura**: internal used-goods search API, filtered to used watch category (中古時計).

Both sources are public web data; only factual product information (name, price, brand, condition) is collected.
