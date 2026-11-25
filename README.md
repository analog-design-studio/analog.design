# analog.design

A static site. No build step, no framework — just HTML files in folders.
GitHub Pages serves this repo at https://analog.design; whatever is on `main`
is what's live.

## Layout

```
CNAME                   tells GitHub Pages the site lives at analog.design
.nojekyll               (already in the repo) tells GitHub Pages to publish the files as they are
index.html              the logo grid
404.html                sends other spellings of an address (/lodge, /WAY) to the right folder
favicon.svg             browser-tab icon: the "a" from the studio logo
logo.svg                the analog design studio logo, bottom-left on every page (links home)
golfa/
  index.html            one scrollable page: description → #privacy → #terms
  assets/golfer.svg     the mark used on the grid
  assets/golfa-logo.svg full logo, used on the golfa page
  privacy/index.html    redirect → /golfa/#privacy
roam/
  index.html            one scrollable page: description → #features → #support → #privacy → #terms
  sphere.svg            the sphere, used on the grid and in the middle of the roam page
  wordmark.svg          the horizontal mark at the top of the roam page
  icon.png              app icon (used as the page's favicon)
  privacy/index.html    redirect → /roam/#privacy
  support/index.html    redirect → /roam/#support
way/
  index.html            one scrollable page: description → #support → #privacy → #terms
  mark.svg              the colour-wheel mark, used on the grid and at the top of the Way page
  mark-offwhite.svg     the same mark in off-white, for dark backgrounds (not used yet)
  pattern.svg           the wheels in offset rows, tiled behind the whole Way page
hew/
  index.html            one scrollable page: description → #support → #privacy → #terms
  icon.svg              the app icon (charcoal "Hew" bottom left on orange), used on the grid and as the tab icon
  mark.svg              the charcoal wordmark alone as a picture (not used: the Hew page now sets "Hew" as text, to match its tagline)
  phone.png             the iPhone that peeks down from the top of the Hew page
LODGE/
  index.html            one scrollable page: description → #support → #privacy → #terms
  icon.png              the app icon (antlers on brown), used as the LODGE page's tab icon
  horns-white.png       the antlers alone in white, at the top of the LODGE page
  horns.png             the antlers alone in LODGE's dark brown, used on the grid
Summed/
  index.html            one scrollable page: description → #support → #privacy → #terms
  icon.png              the app icon ("S."), used on the grid, at the top of the Summed page and as its tab icon
  fonts/                Cardo Regular and Bold (Latin only) for Summed's serif titles, with its licence (OFL.txt)
```

Folder + `index.html` means the URLs are clean: `analog.design/way/`,
`analog.design/way/#privacy`, and so on. The analog logo at the bottom of every page
links back to the grid; swap `logo.svg` to change it everywhere.

## Updating the site

On github.com: open the repo → **Add file → Upload files** → drag in the
changed files or folders (keep the same names and folder structure so they
overwrite the old ones) → **Commit changes**. The live site updates in about
a minute.

To change text: open the page's `index.html` on GitHub, click the pencil,
edit, commit. Each page is one file with its styles at the top and its text
below, in the order it appears on screen.

## App Store buttons

roam, Way and Hew each have a "Download from the App Store" button at the top
right of their pages: the `<a class="store" href="…">` line near the top of the
page. golfa, LODGE and Summed have none. To add one once an app is approved,
copy that line into the page's `<header class="top">`, after the logo's
closing `</a>`, with the app's own App Store link.

## Addresses and capital letters

GitHub Pages treats capitals as different addresses. The apps link to
`analog.design/LODGE/` and `analog.design/Summed/`, so those two folders keep
their capitals. `404.html` sends any other spelling (`/lodge`, `/summed`,
`/WAY`, `/Hew`) to the right folder. When you add a project, add its folder
name to the list at the top of `404.html`.

## Page backgrounds

- **roam**: the stars are drawn by the script at the bottom of
  `roam/index.html`, using the app's own star list and seed. `SIZE`, `ALPHA`
  and `TURN` near the top of that script set how big, how bright and how fast
  they turn as you scroll.
- **Way**: the wheels are `way/pattern.svg`, tiled by the `body::before` rule
  at the top of `way/index.html`. `opacity` sets how faded they are.
- **Hew**: the phone is `hew/phone.png`, cut from the Instagram artwork.

## Adding a project

1. Make a folder: `myapp/`, with an `index.html` — copy `way/index.html` (or
   roam's or golfa's) and swap in your text. Legal and support text lives in
   `<section id="…">` blocks below the description.
2. Put the logo (SVG or PNG) in that folder.
3. In the root `index.html`, copy one of the `<a class="logo">` blocks inside
   `<nav class="grid">`, point it at `/myapp/` and the logo, and add a
   `.logo.myapp img { width: …px; }` rule so it sits at the same visual
   weight as the others.

Logos show greyed-out until hovered; the grid reflows on its own (2 across
on a phone).

## Domain

analog.design is registered at GoDaddy. Its DNS has four A records
(185.199.108.153, .109.153, .110.153, .111.153) and a `www` CNAME to
`analogdesignstudio.github.io`. Nothing there needs to change when the site
is updated.
