# analog.design

A static site. No build step, no framework — just HTML files in folders.
GitHub Pages serves this repo at https://analog.design; whatever is on `main`
is what's live.

## Layout

```
CNAME                   tells GitHub Pages the site lives at analog.design
.nojekyll               (already in the repo) tells GitHub Pages to publish the files as they are
index.html              the home page: one scrolling page with a branded section per app
404.html                sends other spellings of an address (/lodge, /WAY) to the right folder
favicon.svg             browser-tab icon: the "a" from the studio logo
logo.svg                the analog design studio logo, bottom-left on every product page (links home)
golfa/
  index.html            product page: description → #privacy → #terms
  assets/golfer.svg     the golfer, used as golfa's logo in the home page footer
  assets/golfer-white.svg  the golfer in white: large in golfa's section on the home page, then shrinking into its logo
  assets/golfa-logo.svg full logo in green (not used now that the golfa page is green)
  assets/golfa-logo-white.svg  full logo in white, on the golfa page
  assets/golfa-wordmark-white.svg  the same logo without its golfer, in golfa's section on the home page
  privacy/index.html    redirect → /golfa/#privacy
roam/
  index.html            product page: description → #features → #support → #privacy → #terms
  sphere.svg            the sphere, on the roam page and in roam's section on the home page (where it becomes the wordmark's "o")
  sphere-shape.png      the sphere as a one-colour shape, for the home page footer
  wordmark.svg          the horizontal mark at the top of the roam page
  wordmark-open.svg     the same mark without its sphere, in roam's section on the home page
  icon.png              app icon (used as the page's favicon)
  phones/               three iPhone pictures for the home page
  privacy/index.html    redirect → /roam/#privacy
  support/index.html    redirect → /roam/#support
way/
  index.html            product page: description → #support → #privacy → #terms
  mark.svg              the colour-wheel mark: top of the WAY page, its home page section, and the footer
  mark-offwhite.svg     the same mark in off-white, for dark backgrounds (not used yet)
  pattern.svg           the wheels in offset rows, tiled behind the whole WAY page
  phones/               ten iPhone pictures for the home page
hew/
  index.html            product page: description → #support → #privacy → #terms
  icon.svg              the app icon (charcoal "Hew" bottom left on orange), used as the tab icon
  icon-shape.svg        the icon as a one-colour shape, for the home page footer
  mark.svg              the charcoal wordmark alone as a picture (not used: "Hew" is set as text)
  phone.png             the iPhone that peeks down from the top of the Hew page
  phones/               seven iPhone pictures for the home page
LODGE/
  index.html            product page: description → #support → #privacy → #terms
  icon.png              the app icon (antlers on brown), used as the LODGE page's tab icon
  horns-white.png       the antlers alone in white, on the LODGE page and its home page section
  horns.png             the antlers alone, the shape of LODGE's logo in the home page footer
  buck.webp             the buck that opens LODGE's section on the home page, cut out of his photograph
Summed/
  index.html            product page: description → #support → #privacy → #terms
  icon.png              the app icon ("S."), on the Summed page, its home page section, and as the tab icon
  s-shape.png           the S. as a one-colour shape, for the home page footer
  fonts/                Cardo Regular and Bold (Latin only) for Summed's serif titles, with its licence (OFL.txt)
  phones/               six iPhone pictures for the home page
```

Folder + `index.html` means the URLs are clean: `analog.design/way/`,
`analog.design/way/#privacy`, and so on. The analog logo at the bottom of every page
links back to the home page. Product pages show `logo.svg`. The home page has its
own copy of the same drawing inside `index.html` (`<svg class="studio-logo">`), so
that each letter can move on its own; to change the logo, replace both.

## Updating the site

On github.com: open the repo → **Add file → Upload files** → drag in the
changed files or folders (keep the same names and folder structure so they
overwrite the old ones) → **Commit changes**. The live site updates in about
a minute.

To change text: open the page's `index.html` on GitHub, click the pencil,
edit, commit. Each page is one file with its styles at the top and its text
below, in the order it appears on screen.

## App Store buttons and "Coming soon"

roam, WAY, Hew and Summed each have a "Download from the App Store" button at
the top right of their pages: the `<a class="store" href="…">` line near the
top of the page. golfa and LODGE are not in the App Store yet, so they say
"Coming soon" instead and nothing on the site should suggest Apple has
approved them.

When one of them is approved, in two places (its own page, and its section of
the home page `index.html`):

1. Replace `<span class="soon">Coming soon</span>` (on the golfa page,
   `<p class="coming">Coming soon</p>`) with
   `<a class="store" href="APP STORE LINK">Download from the App Store</a>`.
2. LODGE only: its page leaves out one sentence until then. Add
   "The price is shown on LODGE's App Store page." back to the end of the
   "Requirements" paragraph near the top of `LODGE/index.html`.

## The home page

`index.html` is one long scrolling page. Its own notes are at the top of its
styles; the short version:

- **Sections.** Between the opening and the closing there is one
  `<section class="app">` per app, in order: golfa, roam, WAY, Hew, LODGE,
  Summed. Each is several screens tall. `style="--len: 5.2"` on a section is
  how many screens of scrolling it lasts.
- **The opening.** The page starts with the studio logo's eighteen letters
  spread over the whole screen, edge to edge, white with their black 3D edges
  (three rows on a wide screen, three columns on a tall one). Scrolling gathers
  them into the black logo at the bottom left, and the line beside it slides
  over to make room. `--len` on `<section id="top">` is how long that takes;
  part 3 of the script does the work. Each letter is in the page twice:
  `glyph-…` is the logo's own drawing, and `shade-…` is the same letter without
  the logo's fine white outlines, which look like stray slivers when the
  letters are this large. The second fades into the first as the logo forms.
- **The closing.** After Summed, the six app logos rise out of the footer,
  grow, take on their own colours and settle into a grid that fills the screen
  (`<nav class="grid">`; part 4 of the script). Each one opens its app's page.
- **Timing.** Inside a section, anything with `data-at="2.55 3.05"` is on
  screen between those two points, counted in screens scrolled since the
  section took over. `data-fade` is how long it takes to arrive and leave.
  To move a moment earlier or later, change those numbers.
- **Words.** All the copy is plain text inside each section, taken from the
  product pages. Edit it in place.
- **Phones.** The iPhone pictures are in each app's `phones/` folder (cut from
  the Instagram artwork). golfa and LODGE have none yet, so they show empty
  outlines: `<div class="slot"></div>`. To use a real picture, replace a slot
  with `<img class="phone" src="/golfa/phones/NAME.webp" alt="…">`.
- **Header menu.** Each section's header has its logo on the left and a small
  menu on the right: Support, Privacy and Terms (links to those parts of the
  app's page), then the "Download from the App Store" button, or "Coming soon"
  for golfa and LODGE. On phones the menu sits above the button, and where
  the button is too wide to sit beside the logo it drops to a line of its own.
- **Phones.** The rules for narrow screens are in one block near the end of
  the styles ("phones and narrow windows"), with a second short block for
  short phones. Everything keeps clear of the floating letters on the right
  and the footer at the bottom.
- **Capitals.** roam is all lowercase; WAY and LODGE are all capitals; Hew and
  Summed are written normally. For roam, WAY and LODGE the styles enforce it,
  so text typed either way shows correctly.
- **Pieces that travel.** Four things move between two places as you scroll.
  golfa's golfer starts large beside the words and shrinks into the logo at
  the top left, which is drawn without him until he arrives. roam's sphere
  does the same and becomes the "o" of the wordmark. Summed's name starts as
  the word "Summed." across the screen; its period sweeps left over the
  letters until only "S." is left, and that shrinks into the top left corner
  as the logo (`<div class="name">`; `icon.png` takes over from the letters at
  the very end). LODGE's white antlers go the other way: they start out lying
  over the buck's own antlers, then grow and move aside for the words. Each
  travelling piece says where it lines up: `data-joins` names what it joins,
  and `data-spot` is the place on it (centre across, centre down and height,
  each as a share of it). When each one sets off is a number at the top of
  its section's styles: `--tee` (golfa), `--home` (roam), `--sum` (Summed),
  `--turn` and `--part` (LODGE).
- **LODGE's opening.** LODGE's section starts with a buck looking straight at
  you (`<img class="buck">`, `LODGE/buck.webp`: the deer cut out of his
  photograph, on nothing). His antlers turn LODGE white as he sinks back into
  the dark, then the antlers grow and move aside for the words. To use another
  picture, save it over that file (upright, 4 wide by 5 tall, transparent
  background) and change `data-spot` on the `<img class="horns">` line to
  where the new buck's antlers are.
- **Floating pieces.** "DISAPPEARING LIGHT ON A SCREEN" (`<p class="light">`)
  stays off screen during the opening, comes up with golfa's section, then
  climbs slowly down the right side and fades at the top. The studio logo,
  its line (`<p class="tagline">`) and the six app logos (`<nav class="dock">`)
  stay at the bottom. The app logos are drawn in one colour that follows the
  section behind them; tapping one jumps to that app's section.
- **Motion.** `--m` at the top of the styles scales all drift and tilt
  (1 = full, 0 = none). Visitors who have asked their device for reduced
  motion get 0 automatically.

To add an app: copy a section, give it a new `id`, add a link to it in the
dock (changing `repeat(6, …)` in `.dock` to the new count), and add a tile for
it in the closing grid.

## Addresses and capital letters

GitHub Pages treats capitals as different addresses. The apps link to
`analog.design/LODGE/` and `analog.design/Summed/`, so those two folders keep
their capitals. `404.html` sends any other spelling (`/lodge`, `/summed`,
`/WAY`, `/Hew`) to the right folder. When you add a project, add its folder
name to the list at the top of `404.html`.

## Page backgrounds

- **roam**: the stars are drawn by a script, using the app's own star list and
  seed. On the roam page it is at the bottom of `roam/index.html` (`SIZE`,
  `ALPHA`, `TURN`); on the home page it is part 6 of the script in `index.html`
  (`STAR_SIZE`, `STAR_ALPHA`, `TURN`).
- **WAY**: on the WAY page the wheels are `way/pattern.svg`, tiled by the
  `body::before` rule at the top of `way/index.html`; `opacity` sets how faded
  they are. On the home page the wheels are drawn and turned by part 7 of the
  script in `index.html` (`SPIN` is how fast they turn; `.way canvas` sets how
  faded they are).
- **Hew**: the phone on the Hew page is `hew/phone.png`, cut from the Instagram
  artwork.

## Adding a project

1. Make a folder: `myapp/`, with an `index.html` — copy `way/index.html` (or
   roam's or golfa's) and swap in your text. Legal and support text lives in
   `<section id="…">` blocks below the description.
2. Put the logo (SVG or PNG) in that folder.
3. On the home page (`index.html`), copy one app's `<section class="app">`,
   give it a new `id`, colours and words, then add a link to it in
   `<nav class="dock">` (changing `repeat(6, …)` in `.dock` to the new count)
   and a tile in `<nav class="grid">`.
4. Add the folder's name to the list at the top of `404.html`.

## Domain

analog.design is registered at GoDaddy. Its DNS has four A records
(185.199.108.153, .109.153, .110.153, .111.153) and a `www` CNAME to
`analogdesignstudio.github.io`. Nothing there needs to change when the site
is updated.
