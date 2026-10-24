# 2Six2 Services – An online automotive shop

Product catalogue and cart for **2Six2 Services** are embedded in the company's Google Sites' website where customers can browse products, add them to a cart and send their order by email from their email account.

> Given that **this repository is public**, its content and history can be seen by anyone so never add customer details, passwords, spreadsheet edit links or other private files.

## Live URLs

| What | URL |
|---|---|
| Shop – all products | `https://2Six2Services.github.io/2six2-services/shop/` |
| Shop – one category | `https://2Six2Services.github.io/2six2-services/shop/?category=Interior%20Parts%20&%20Accessories` |
| Shop – one product | `https://2Six2Services.github.io/2six2-services/shop/?product=Luxury%20Steering%20Wheel%20Cover` |
| Images | `https://2Six2Services.github.io/2six2-services/images/` |

## What's in this repository

```
2six2-services/
├── index.html          redirects to shop/
├── shop/
│   └── index.html      the shop (single file: layout, styles and code)
├── images/
│   ├── brand/          logo and other brand images
│   └── products/       one folder per product
├── .gitignore          keeps original photos and system files out of the repository
├── .nojekyll           instructs GitHub Pages to publish files exactly as they are
├── LICENSE             all rights reserved
└── README.md
```

## Adding and changing products

Products come from the **Products** tab of the company's Google Sheet, which is published to the web
as CSV (File → Share → Publish to web). The shop reads that published copy only while the main spreadsheet remains
private. The published link is set as `SHEET_CSV_URL` in `shop/index.html`.

- **One row per size.** Repeat the product name on a new row for each size.
- **Only shop information belongs in the Products tab.** since everything within it is public once published.
- **Changes appear within about 5 minutes** when Google refreshes the published copy.

| Column | Required | What to enter |
|---|---|---|
| Product | yes | Product name, e.g. `Luxury Steering Wheel Cover` |
| Category | | e.g. ` Interior Parts & Accessories` – groups products, and sets Previous/Next and Related |
| Size | | e.g. `Small`, `Large` – blank means "One size" |
| Price | | Number, e.g. `1200` |
| Quantity | | Stock count – `0` shows "Out of stock" |
| Description | | One feature per line in the cell: `Quick access - biometric lock` (text before ` - ` is shown in bold) |
| Image | | One or more image URLs, one per line or separated by commas – the first is used on the product card |
| Related | | Optional, comma-separated product names – blank shows other products in the same category |
| ID | | Optional unique key, only needed if two products share a name |
| Link | | Optional – only used for Previous/Next/Related products that aren't in the list |

## Adding images

1. **Resize photos first**: about 1200–1600 px wide, JPEG or WebP, ideally under 300 KB each.
2. **Name them by the rules below** and put them in `images/products/<product-slug>/`.
3. **Upload** them to this repository (Add file → Upload files → Commit changes). Changes go through a pull request
4. **Paste the image URL into the product's `Image` cell** in the sheet, for example:
   `https://2Six2Services.github.io/2six2-services/images/products/interior-parts-accessories/luxury-steering-wheel-cover-1.jpg`

Naming rules:

- **Lowercase letters, numbers and hyphens only**: `luxury-steering-wheel-cover-1.jpg`, not `Luxury Steering Wheel Cover (1).JPG`.
- **File names are case-sensitive.** `.JPG` and `.jpg` are different files – use lowercase `.jpg`.
- **No spaces, underscores or special characters.**
- **Folder = product slug** (the product name in lowercase with hyphens). No category in the path, so images keep working if a product changes category.
- **Number the photos** `-1`, `-2`, `-3` … in the order they should appear in the product's image carousel.
- **Replacing a photo but keeping the old one?** Add `-v2` to the new file name.
- **Keep full-size originals out of the repository.** A folder named `originals/` is ignored by `.gitignore`.

Products without an image, or with a broken image link, show a grey "No image available" placeholder.

## Embedding in Google Sites

Use **Insert → Embed → By URL** (not "Embed code") and paste one of the shop URLs. One Sites page per view:

| Google Sites page | Embed URL |
|---|---|
| Products (all) | `.../2six2-services/shop/` |
| A category page | `.../2six2-services/shop/?category=Interior%20Parts%20&%20Accessories` |
| A single product | `.../2six2-services/shop/?product=Luxury%20Steering%20Wheel%20Cover` |

- **Category and product names** must match the sheet (capitals don't matter). Write spaces as `%20`.
- **Every page shares one cart**, because all embeds load from the same address.
- **Make the embed box tall** in the Sites editor; content taller than the box scrolls inside it.
- **The embed is only clickable in Preview and on the published site** – the Sites editor covers embeds so they can be moved and resized.

The "Embed code" option won't work with `?category=` or `?product=`, because Google hosts pasted code at its
own address and doesn't pass these options to it.

## Settings

At the top of the script in `shop/index.html`:

| Setting | Purpose |
|---|---|
| `SHEET_CSV_URL` | Published CSV link of the Products tab |
| `ORDER_EMAIL` | Address customers send their order emails to |
| `CURRENCY_PREFIX`, `CURRENCY_SUFFIX` | How prices are shown, e.g. `$` … `EC` |
| `IS_CATEGORY_FILTER_ON`, `CATEGORY_FILTER` | Limit the shop to one category (a `?category=` in the URL overrides this) |
| `LIST_OPENS_FULL_DETAILS` | `true` = full details page (carousel, Previous/Next, Related); `false` = simple view |
| `RELATED_MAX` | Number of related products on a details page |

Changes pushed to this repository go live on GitHub Pages within a few minutes.

## Privacy

- **No customer details are collected or stored.** Customers write and send the order email themselves; the page only prepares the text.
- **The cart is kept in the visitor's own browser** (products, sizes and quantities only).
- **No analytics, cookies, trackers or web fonts.**
- **The page loads data from Google** (the published product list and any images hosted there) and from this site.

## Licence

All rights reserved. Logos and brand names belong to 2Six2 Services while most product images are the property of their respective owners and used for illustration purposes only. See [LICENSE](LICENSE).
