# Personal academic website

Four static pages, one stylesheet, no build step. Nothing here needs to be
compiled, installed or run — the files you edit are the files that get served.

```
index.html        home: photo, profile, feature panel, research, teaching, links
research.html     papers and preprints, theses, talks
writing.html      expository writing, lecture notes, teaching materials
exposition.html   the long-form expository article
css/style.css     the only stylesheet
images/           see images/README.md for file names and sizes
.nojekyll         tells GitHub Pages to serve the files as-is
```

## Filling in the placeholders

Every piece of text you need to replace is wrapped in double curly braces:

```html
<h2>{{ SECTION HEADING }}</h2>
```

So to find everything still outstanding, search the repository for `{{`:

```sh
grep -rn "{{" *.html          # or use your editor's find-in-files
```

The site is finished when that returns nothing.

Repeatable blocks are marked with HTML comments like
`<!-- Repeat this block for each paper -->`. Copy the whole `<li class="entry">…</li>`
and edit the copy. Delete any placeholder blocks you do not need — three papers
and three talks are shipped as examples, not as a minimum.

## Previewing locally

Double-click any `.html` file. It will open from `file://` and render correctly,
including the maths — everything uses relative paths.

If you would rather have a real server (so that links behave exactly as they will
once deployed), run this from the repository root:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000>. Stop it with Ctrl-C.

## Images

Put them in `images/` — see `images/README.md` for the expected file names,
export sizes, and a note on why diagrams should be SVG or PNG rather than JPEG.
Until you add the files, the pages show broken-image icons. That is expected.

## Adding a paper or a talk

Open `research.html`, find the block comment, and copy the entry above or below it:

```html
<li class="entry">
  <p class="entry__title"><a href="https://arxiv.org/abs/2501.00000">Title of the paper</a></p>
  <p class="entry__meta">with A. Coauthor · arXiv:2501.00000</p>
  <p>One line on what it does.</p>
</li>
```

Every line except the title is optional — delete the `entry__meta` line for a
sole-authored preprint with no reference yet, or the last line if you do not want
a description. Talks and lecture notes work the same way; the class names differ
only in what they are called.

## Changing the colour scheme

Open `css/style.css`. The first block in the file is a `:root` block holding every
colour, spacing value and column width the site uses. Edit those values and the
change propagates everywhere — nothing further down the file hard-codes a colour
or a size.

```css
:root {
  --color-accent: #24578c;   /* links, and the left edge of the feature panel */
  --measure: 70ch;           /* width of the prose column */
  ...
}
```

Directly below it is a `@media (prefers-color-scheme: dark)` block that overrides
the same custom properties for readers whose system is set to dark mode. If you
change a colour in one block, change its counterpart in the other. To drop dark
mode entirely, delete that block.

## Mathematics

`research.html` and `exposition.html` load KaTeX from a CDN (with subresource
integrity hashes) and render `$…$` inline and `$$…$$` as display maths. The other
two pages do not load it at all, so they stay fast and dependency-free.

`exposition.html` contains a short demo block, marked in the source, showing both
delimiters — delete it once you have seen it render. To escape a literal dollar
sign in prose, write `\$`.

To upgrade KaTeX later, change the version number in the three CDN URLs and
regenerate the `integrity` hashes; mismatched hashes will silently block the
scripts from loading.

## Publishing on GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*.
4. Choose branch `main` and folder `/ (root)`. Save.
5. Wait a minute, then load `https://YOUR-USERNAME.github.io/YOUR-REPO/`.

If the repository is named `YOUR-USERNAME.github.io`, the site is served from
`https://YOUR-USERNAME.github.io/` instead.

The empty `.nojekyll` file stops GitHub from running the pages through Jekyll.
Leave it in place — without it, any file or folder beginning with an underscore
would be silently dropped.

## Using your own domain

1. Create a file called `CNAME` in the repository root containing only the domain,
   with no protocol and no trailing slash:

   ```
   www.example.com
   ```

2. At your DNS provider, add a `CNAME` record for `www` pointing at
   `YOUR-USERNAME.github.io`. For a bare domain (`example.com`) add `A` records
   pointing at GitHub's four IP addresses instead — the current list is in
   GitHub's Pages documentation under "Managing a custom domain".
3. Back in **Settings → Pages**, enter the domain under **Custom domain**, and
   tick **Enforce HTTPS** once the certificate has been issued (this can take up
   to an hour).

## Accessibility notes

The markup already gives you semantic landmarks, a skip-to-content link, one `<h1>`
per page, and a visible keyboard focus ring. Two things are left to you: write real
`alt` text for every image, and keep the heading order intact — an `<h3>` should
only ever sit under an `<h2>`.