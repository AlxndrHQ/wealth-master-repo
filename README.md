# AlxndrHQ — Master Index

One front door to every sister project. `index.html` is a single static page, styled like the other sites, that links to each project's live GitHub Pages site and its repo.

| # | Project | Live site | Repo |
|---|---|---|---|
| 01 | Algos & Capital | https://alxndrhq.github.io/historical-wealth-mind-map/ | [historical-wealth-mind-map](https://github.com/AlxndrHQ/historical-wealth-mind-map) |
| 02 | Old Money | https://alxndrhq.github.io/european-wealth-map/ | [european-wealth-map](https://github.com/AlxndrHQ/european-wealth-map) |
| 03 | The Triangle Trade | https://alxndrhq.github.io/triangle-trade-mind-map/ | [triangle-trade-mind-map](https://github.com/AlxndrHQ/triangle-trade-mind-map) |
| 04 | HBCU Legacy Web | https://alxndrhq.github.io/hbcu-legacy-mind-map/ | [hbcu-legacy-mind-map](https://github.com/AlxndrHQ/hbcu-legacy-mind-map) |
| 05 | Black Business Directory | https://alxndrhq.github.io/black-business-directory/ | [black-business-directory](https://github.com/AlxndrHQ/black-business-directory) |
| 06 | Ground Truth | https://alxndrhq.github.io/pg-county-land-map/ | [pg-county-land-map](https://github.com/AlxndrHQ/pg-county-land-map) |

## Adding a project

Add an entry to the `GROUPS` array near the bottom of `index.html` (`name`, `sub`, `repo`, `desc`, and optionally `hue` and a `path` such as `#/map`).

## Linking back from each site

Each sister site's header has a row of mono uppercase links (`.tabs button`, `.theme`). Put this link in that row to come back here:

```html
<a class="theme" href="https://alxndrhq.github.io/wealth-master-repo/" title="All projects">← All projects</a>
```

Replace the URL with this repo's Pages URL if you name the repo something else.

## Theme

The page uses the same `theme` localStorage key as the sister sites. They are all served from `alxndrhq.github.io`, so choosing light or dark on one site applies to all of them.
