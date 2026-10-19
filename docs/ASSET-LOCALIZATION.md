# Asset localization

Source: user-supplied full-page PNG and 16-page PDF capture of the linked product page. The PNG is only 224 × 2048 pixels. The PDF provides substantially sharper raster artwork.

The short URL redirected to Facebook during direct retrieval and browser inspection. Retrieval of the complete supplied URL later recovered the original product HTML and all 49 unique source image assets, including 7 animated GIFs. These are retained in `source-media/manifest.json` order. Original GIF frames, timing and embedded source-language lettering are preserved, with English labels in the interface. Main English promotional artwork remains localized from the PDF reference. Original image sections were extracted from the embedded PDF raster data and are retained under `reference-originals/` in page order.

Built-in image editing was used for English text localization. Prompt set: replace Chinese writing with accurate legible English; preserve photos, people, products, palette, frames, section ordering and proportions; preserve prices and numeric readings; retain source testimonials as attributed customer claims. Product name: Organic Islet Fruit Tea / Jerusalem Artichoke. Original labels and photographic details may still differ, particularly across page boundaries.

Native React components replace the screenshot's price card and final order form. Package quantities and checkout prices were read from the high-resolution original checkout capture. Currency remains NT$ / TWD, matching the reference. Taiwan city and county names are in English. The district and pickup store are entered as text rather than relying on a merchant's unavailable store-lookup API.

`frontend/public/assets/panel-00.webp` through `panel-14.webp`: English localized artwork. First and final artwork sections are clipped by responsive CSS so native purchasing components replace their raster equivalents. `frontend/src/panels.json`: source order, dimensions and accessible section descriptions. No stock media was substituted for source videos.
