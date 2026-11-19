# analog.design

A static site. No build step, no framework — just HTML files in folders.
GitHub Pages serves this repo at https://analog.design; whatever is on `main`
is what's live.

## Layout

```
CNAME                   tells GitHub Pages the site lives at analog.design
.nojekyll               (already in the repo) tells GitHub Pages to publish the files as they are
index.html              the logo grid
favicon.svg             browser-tab icon for the home page: the "a" from the analog logo
logo.svg                the analog logo, bottom-left on every page (links home)
golfa/
  index.html            one scrollable page: description → #privacy → #terms
  assets/golfer.svg     the mark used on the grid
  assets/golfa-logo.svg full logo, used on the golfa page
  privacy/index.html    redirect → /golfa/#privacy
roam/
  index.html            one scrollable page: description → #features → #support → #privacy → #terms
  sphere.svg            the mark used on the grid
  wordmark.svg          the horizontal mark at the top of the roam page
  icon.png              app icon (used as the page's favicon)
  privacy/index.html    redirect → /roam/#privacy
  support/index.html    redirect → /roam/#support
way/
  index.html            one scrollable page: description → #support → #privacy → #terms
  mark.svg              the colour-wheel mark, used on the grid and at the top of the Way page
  mark-offwhite.svg     the same mark in off-white, for dark backgrounds (not used yet)
hew/
  index.html            one scrollable page: description → #support → #privacy → #terms
  icon.svg              the app icon (charcoal "Hew" bottom left on orange), used on the grid and as the tab icon
  mark.svg              the charcoal wordmark alone, used at the top of the orange Hew page
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

roam and Way have a "Download from the App Store" button at the top right of
their pages: the `<a class="store" href="…">` line inside `<header class="top">`.
To add one to another page (Hew has a commented-out line ready), put the same
line there with that app's App Store link.

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
