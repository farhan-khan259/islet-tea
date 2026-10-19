# Organic Islet Fruit Tea — English landing page

React + Vite frontend, Node.js + Express API, MongoDB order persistence. Separate frontend and backend folders. The original page is largely promotional artwork, so the reconstruction uses localized image panels and native React purchasing components.

## Run locally

Requires Node.js 20.19+ or 22.12+ and MongoDB 7+.

```bash
npm ci
cp backend/.env.example backend/.env
```

Set MongoDB and admin credentials in `backend/.env`. On Windows, copy that file using File Explorer or `Copy-Item`. From the backend directory run `npm run dev` so dotenv loads its `.env`, or export the variables before the root command. The root development command loads the workspace backend process with the backend working directory.

```bash
npm run dev
```

Open http://localhost:5173. Vite proxies `/api` to port 4000. Orders require MongoDB; the frontend remains viewable without it and clearly reports unavailable ordering. No mock order is reported as a real submission.

## Production

```bash
npm run build
npm start
```

Open http://localhost:4000 (also `/product.html`). Express serves the built React frontend and API together. Configure HTTPS at your reverse proxy. Set `FRONTEND_ORIGIN` to your domain. If a reverse proxy is used, configure Express trust proxy narrowly for your infrastructure before relying on IP rate limiting.

Alternatively, set `ADMIN_API_KEY` in your shell and run `docker compose up --build`. MongoDB is internal to the Docker network; its data persists in a volume. Backup that volume before removing it.

## API

- `GET /api/products/organic-islet-fruit-tea`: authoritative product/package catalog.
- `GET /api/health`: process and database configuration status.
- `POST /api/orders`: validated, server-priced order creation. Send `Idempotency-Key` UUID header. The form does this automatically. Repeat submissions reuse the order, not a second purchase.
- `GET /api/admin/orders?page=1`: list recent orders; requires `X-Admin-Key`. Never put this key in frontend code. No public customer lookup endpoint exposes order details.

The API ignores client prices, rejects invalid packages/delivery methods, rate limits submissions and limits request size. Cash on delivery only; no card payment integration is implied. Convenience-store pickup collects store details but is not integrated with carrier/store APIs.

## Edit content and assets

`backend/src/catalog.js` contains package prices and videos. Keep `frontend/src/catalog.js` (offline catalog display) synchronized if changing prices. The API remains authoritative for submitted totals. Source prices retained: NT$998 display price, NT$1,598 comparison price; checkout packages 8/4/2/6/12 jars at NT$1,650/1,250/1,050/1,450/1,898.

`frontend/public/assets/panel-00.webp` through `panel-14.webp` are English-localized promotional panels. `frontend/src/panels.json` describes their sequence and dimensions. `frontend/src/components` contains separate React components. All CSS is in `frontend/src/styles.css`.

## Original videos and localization limits

The short URL redirected to Facebook. A later retrieval using the full supplied URL recovered the original product HTML and all 49 unique source image assets. The source page contains **7 animated GIFs** and no HTML video/source elements or linked MP4 files. These GIFs are retained in `source-media/` for reference but are not displayed on the page. The main promotional panels are English-localized still artwork. Full frame-by-frame translation of baked-in GIF lettering is not completed.

The original source's apparent video-player thumbnails are part of static JPEG artwork. They are not functional video players, and no false playback controls were added to those stills. The source HTML's tracking scripts, fingerprinting and anti-debug code were not copied into this app.

To add actual videos, put the MP4 and an English WebVTT file in `frontend/public/assets/` and add entries to `product.media.videos`:

```js
{ src:'/assets/original-video-1.mp4', poster:'/assets/video-1-poster.webp', captions:'/assets/video-1-en.vtt', title:'Farm visit' }
```

Videos then render with native playback, mobile inline support and captions. They are appended after the promotional story. Adjust `Story.jsx` to insert individual videos at their exact original positions if separate video media is supplied.

Image text was localized with the built-in image editing tool, preserving the reference's overall composition. This is a close reconstruction, not a certified pixel-identical translation: English wrapping, small labels, AI typography and photographed details can differ. Source health claims, testimonials, certification images and sales counts remain reference marketing content; they were not independently verified. Review translations and factual claims before commercial publication. No real merchant identity, fulfillment agreement or external checkout service was invented.

## Checks

```bash
npm test
npm run build
```

See `docs/VERIFICATION.md` for actual results and verification limits.
# islet-tea
