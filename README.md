# Alexander Stepanov — Portfolio

A minimal one-page portfolio built with **Vite** and **Tailwind CSS v4**.

## Run Locally

```bash
npm install
npm run dev
```

Open `http://localhost:5173` in your browser.

## Build for Production

```bash
npm run build
```

Output is in the `dist/` folder.

## Deploy to Vercel

1. Push this repo to GitHub.
2. Go to [vercel.com](https://vercel.com), import the repository.
3. Vercel auto-detects Vite — just click **Deploy**.

## Deploy to GitHub Pages

1. Install the gh-pages package:
   ```bash
   npm install -D gh-pages
   ```
2. Add to `package.json` scripts:
   ```json
   "deploy": "npm run build && gh-pages -d dist"
   ```
3. Set `base` in `vite.config.js` to your repo name:
   ```js
   export default { base: '/your-repo-name/', ... }
   ```
4. Run `npm run deploy`.

## CV

Place your CV file as `public/cv.pdf` — it will be served at `/cv.pdf`.
