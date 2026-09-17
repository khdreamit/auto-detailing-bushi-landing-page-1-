# Auto Detailing Bushi — Landing Page

A premium, single-page landing page for **Auto Detailing Bushi**, an
automotive detailing business in Farke e Madhe, Tiranë, Albania. Built with
React, Vite, and Tailwind CSS.

## 1. Project Overview

This is a single-page site (`/`) with smooth-scrolling sections: hero, trust
strip, about, services, gallery, reviews, FAQ, a booking form, and contact
details. All business information (phone, address, social links, Google
Maps URL, reviews) comes only from what was supplied by the client — nothing
has been invented (no fake prices, hours claims, staff counts, etc).

**Tech stack:** React 18 · Vite 5 · Tailwind CSS 3 · lucide-react icons.

> **Note on this build:** this project was assembled in an offline
> environment without access to the npm registry, so `npm install` could
> not be executed here to produce a `node_modules` folder or a verified
> `dist/` build. Every source file was checked individually with esbuild for
> syntax/import correctness, but you should still run the steps in section 2
> once on your machine (with internet access) to install dependencies and
> confirm the production build.

## 2. Installation

You'll need [Node.js](https://nodejs.org) 18 or newer.

```bash
# 1. Unzip the project and move into it
cd auto-detailing-bushi

# 2. Install dependencies
npm install

# 3. Run the local dev server
npm run dev
```

Open the URL Vite prints (usually `http://localhost:5173`) to view the site.

## 3. Building for Production

```bash
npm run build
```

This outputs a production-ready static site to the `dist/` folder. You can
preview that build locally with:

```bash
npm run preview
```

Deploy the contents of `dist/` to any static host (Netlify, Vercel, cPanel,
GitHub Pages, etc.).

## 4. Editing Content

Almost all editable business content lives in **one file**:

```
src/data/business.js
```

### Change the phone number
Edit `phoneDisplay` (what's shown on screen) and `phoneHref` (the `tel:`
link, digits only, no spaces) in `src/data/business.js`.

### Change the Facebook link
Edit `facebookUrl` in `src/data/business.js`.

### Change the Instagram link
Edit `instagramUrl` in `src/data/business.js`.

### Change the Google Maps URL
Edit `googleMapsUrl` in `src/data/business.js`. This single value powers
every "View on Google Maps" / "Get Directions" button on the site, plus the
structured data (SEO) in `index.html`.

### Replace gallery images
1. Add your new images to `public/images/`.
2. Update the `galleryImages` array in `src/data/business.js` — each entry
   needs a `src` (path starting with `/images/`) and a descriptive `alt`
   text for accessibility.
3. The same applies to `hero.jpg`, `about.jpg`, and `featured.jpg`, which
   are referenced directly inside `src/components/Hero.jsx`,
   `src/components/About.jsx`, and `src/components/FeaturedSection.jsx`.

### Edit services
Edit the `services` array in `src/data/business.js` — add, remove, or
reword entries freely. Each service needs an `id`, `title`, and
`description`. If you add a brand-new `id`, also add a matching icon for it
in the `icons` map at the top of `src/components/Services.jsx` (pick any
icon name from [lucide.dev/icons](https://lucide.dev/icons)).

### Edit the FAQ
Edit the `faqs` array in `src/data/business.js` — each entry needs a
`question` and `answer`.

### Edit reviews
Edit the `reviews` array in `src/data/business.js`. Only add reviews that
are genuinely posted on Google — do not invent review text or ratings.

## 5. The Booking Form

The "Request a Detailing Service" form (`src/components/BookingForm.jsx`)
is a **frontend-only** form. It validates required fields and shows a
confirmation message, but it does not currently send data anywhere. To
connect it to a real inbox, wire the `onSubmit` handler up to an email
service (e.g. Formspree, EmailJS) or your own backend endpoint.

## 6. Project Structure

```
auto-detailing-bushi/
├── index.html
├── package.json
├── vite.config.js
├── tailwind.config.js
├── postcss.config.js
├── public/
│   └── images/          ← all photography used on the site
├── src/
│   ├── main.jsx
│   ├── App.jsx           ← assembles all sections in order
│   ├── index.css
│   ├── data/
│   │   └── business.js   ← single source of truth for editable content
│   └── components/       ← one component per section
└── README.md
```

## 7. Deploying the Site (Important — GitHub alone will not show it live)

Uploading this project to a **GitHub repository only stores the code** — it
does not run it. GitHub doesn't execute `npm install`/`npm run build` or
serve a React app on its own, so visiting your repo (or the raw files) will
never show the working site. You need one extra step:

### Option A — Vercel or Netlify (easiest, recommended)
1. Push this project to a GitHub repository.
2. Go to [vercel.com](https://vercel.com) or [netlify.com](https://netlify.com), sign in, and choose "Import from GitHub."
3. Select your repository. Both platforms auto-detect Vite — build command
   `npm run build`, output folder `dist`.
4. Deploy. You'll get a live URL in about a minute, and it auto-redeploys
   every time you push to GitHub.

### Option B — GitHub Pages
GitHub Pages can host it too, but Vite needs to know the site won't live at
the domain root — it'll live at `https://<username>.github.io/<repo-name>/`.
1. In `vite.config.js`, add the `base` option:
   ```js
   export default defineConfig({
     plugins: [react()],
     base: "/<repo-name>/", // replace with your actual repo name
   });
   ```
2. Install the deploy helper and add a script:
   ```bash
   npm install --save-dev gh-pages
   ```
   Then add to `package.json` under `"scripts"`:
   ```json
   "deploy": "vite build && gh-pages -d dist"
   ```
3. Run `npm run deploy`. In your repo's Settings → Pages, set the source to
   the `gh-pages` branch.

If you skip the `base` setting, the deployed page will load with broken
CSS/images (a common "GitHub Pages shows a blank/broken page" symptom for
Vite projects).

## 8. Accuracy Note

Every fact on this site (address, phone number, rating, review count,
review author names, social links, Google Maps URL, "open 24 hours" status)
is taken directly from information supplied for this project. Service
categories are presented as editable, general offerings rather than a
guaranteed price list — update `src/data/business.js` as the business's
actual services or details change.
