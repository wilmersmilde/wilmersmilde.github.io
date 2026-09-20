# images/

Every image the site expects lives here. None of them exist yet, which is why the
pages currently show broken-image icons with the alt text next to them. Drop the
files in with exactly these names and the icons disappear.

| File name        | Used on                      | Export at        | Displayed at |
| ---------------- | ---------------------------- | ---------------- | ------------ |
| `headshot.jpg`   | `index.html`                 | ~560 × 700 px    | 280 px wide  |
| `feature.jpg`    | `index.html`, `writing.html` | ~640 px wide     | ~40% of column |
| `figure-01.jpg`  | `exposition.html`            | ~1000 px wide    | full column  |
| `figure-02.jpg`  | `exposition.html`            | ~1000 px wide    | full column  |
| `figure-03.jpg`  | `exposition.html`            | ~1000 px wide    | full column  |

Export at roughly twice the displayed width so the images stay sharp on retina
screens.

## Notes

- **Keep the file names or change them in both places.** If you rename a file,
  update the `src` in the HTML and the `width`/`height` attributes to match the
  new aspect ratio. Those attributes stop the page from jumping while images load.
- **Diagrams are better as SVG or PNG than JPEG.** Line drawings, TikZ output and
  plots compress badly as JPEG and pick up fuzzy edges. Save them as
  `figure-01.svg` (or `.png`) and change the `src` accordingly.
- **Keep files under about 300 KB.** GitHub Pages serves them directly with no
  optimisation step, so whatever you commit is what visitors download.
- **Write real alt text.** Each `alt` attribute in the HTML currently holds an
  instruction to you. Replace it with a sentence describing what the picture
  shows — for a figure, describe what the reader should notice, not just its title.
- Adding more figures to the exposition page: copy the figure block marked
  `<!-- Repeat this figure block for each picture -->` and name the file
  `figure-04.jpg`, and so on.
