# Safety-LAD release site

Static website for the Safety-LAD data set: https://andrew-b-park.github.io/safety-lad/
The data set is published on NYU UltraViolet: https://doi.org/10.58153/t00gt-xer32
The data itself lives on NYU UltraViolet; this site shows what the data set
contains and links to each download bundle.

- `index.html`: the whole site (vanilla JS, no build step)
- `data/<cell>.json`: one file per cell (scene group x ladder type, and `real`): frame ids, verdicts, measurements, boxes and keypoints
- `data/index.json`: slim browse index of the 20,000 generated frames (ids, verdicts, rule verdict codes, splits, violation types, angle), read first so the page shows frames before any cell file loads; a cell's full file is fetched when one of its frames is opened, and `real.json` only in the real view (built by `sdg/release/site/build_browse_index.py` in the main repo; rebuild it whenever `data/` changes)
- `t/<cell>/NNN.webp`: thumbnail sheets, 100 frames each
- `t/overview/NNN.webp`: the first 300 tiles of all generated frames in the page's mixed order, so the opening pages need one sheet instead of 24 (built by `sdg/release/site/build_overview_sheets.py` from the cell sheets; run it before `build_browse_index.py`, which copies its `t/overview/index.json` into the browse index)
- `d/<cell>/<id>.webp`: detail sprite per frame, views stacked top to bottom (generated: photorealized, render, semantic, depth, normals; real: photo, masks)
- `c/<cell>/<id>.webp`: Canny edge preview per generated frame, from the sealed release's `control_canny` (built by `sdg/release/site/build_canny_views.py` in the main repo)
- `CITATION.cff`: citation metadata (GitHub shows a "Cite this repository" button)

File names and the download list link to the record's files (`LINKS_LIVE` in `index.html`), and the DOI
is a link on the page, in its JSON-LD and in `CITATION.cff`. The site is served by GitHub Pages from the
main branch. The large viewer images come from two separate media sites; if they cannot be reached the
viewer shows the smaller previews kept in this repository.
