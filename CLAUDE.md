# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static GitHub Pages website for the TACO Group (Trustworthy, Autonomous, Human-Centered, and Embodied Intelligence Group) at Texas A&M University. Hosted at `taco-group.github.io`.

## Tech Stack

- Plain HTML5 pages (no templating engine, no static site generator)
- Bootstrap 4.4.1 + jQuery 3.3.1
- SCSS source in `scss/`, compiled CSS in `css/style.css`
- JavaScript plugins: Owl Carousel, AOS (scroll animations), Stellar.js (parallax), Sticky.js, Fancybox (lightbox)
- Font Awesome 5.15.4 + Academicons for icons

## Development

No build system, package manager, or CI/CD pipeline. The site is pure static files committed directly to `main` and served by GitHub Pages.

**SCSS compilation:** The `scss/style.scss` file is the source; `css/style.css` is the compiled output. If editing styles, modify SCSS files and recompile:
```bash
sass scss/style.scss css/style.css
```

## Architecture

All pages are standalone HTML files sharing a common header/nav/footer structure copied across files (no includes or partials):

| Page | File | Purpose |
|------|------|---------|
| Home | `index.html` | News, highlights, sponsor logos |
| Publications | `publication.html` | Papers organized by year/type |
| Teaching | `teaching.html` | Course listings |
| Group | `group.html` | Team member profiles |
| Resource | `resource.html` | Resources and links |
| Citation Map | `citation_map.html` | Generated Leaflet.js/D3.js map (via `citationmap.py`) |

Additional pages exist but are **not linked in the nav**: `research.html`, `prospective_students.html`.

The `meranda/` directory is a standalone event page (LID workshop) with its own structure — it is independent from the main site.

**Navigation** is defined in each HTML file's `<nav>` block — changes to nav must be replicated across **all** pages (index, publication, teaching, group, resource, citation_map, research, prospective_students).

## Key Directories

- `groups/` — Team member photos
- `files/publications/` — Publication PDFs
- `files/images/` — Miscellaneous images
- `css/` — Compiled stylesheets and vendor CSS
- `scss/` — SCSS source files (entry: `style.scss`)
- `js/` — JavaScript libraries and `main.js` (site initialization)
- `fonts/` — Icon fonts (icomoon, flaticon)

## Common Tasks

### Adding a news entry

Edit `index.html`. News entries live inside `<div class="trend-entry d-flex"><div class="trend-contents">`. Each month block follows this pattern:

```html
<b style="color:rgb(40, 40, 40)">[Mon YYYY]</b>
<ul style="margin-bottom:5px">
    <li>Summary line (e.g., "2x ACL 2026 accepted. Cheers!")</li>
    <ul style="margin-bottom:5px">
        <li><a href="https://arxiv.org/abs/...">Paper Title</a></li>
        <li>[Tag] Paper Title (if no link yet)</li>
    </ul>
</ul>
```

Add new months **at the top** of the trend-contents div (reverse chronological).

### Adding a publication

Edit `publication.html`. Publications are grouped by year under section headers. Each entry is a `<li>` inside `<div class="trend-entry d-flex"><div class="trend-contents"><ul>`:

```html
<li>Author1, Author2, ..., and AuthorN
<br> <b style="color:rgb(71, 71, 71)">"Paper Title"</b>
<br>Venue Year. <a href="URL">[Paper]</a> <a href="URL">[Code]</a></li>
```

Common link labels: `[Paper]`, `[Code]`, `[Project]`, `[Dataset]`. Upload PDFs to `files/publications/`.

### Adding a group member

Edit `group.html`. Members use Bootstrap `col-md-3` cards. Add photo to `groups/`. Student card template:

```html
<div class="col-md-3" style="margin-bottom: 40px">
    <div class="card">
        <a href="HOMEPAGE"><img src="groups/PHOTO.jpg" width="100%" style="margin:auto"></a>
        <div class="post-meta">
            <span class="d-block" style="padding-top:10px">
                <a href="HOMEPAGE">Full Name</a>
            </span>
            <span class="d-block"> (Fall YYYY - ) </span>
            <a href="SCHOLAR_URL"><i class="ai ai-google-scholar-square ai-1x"></i> Google Scholar</a>
            <span class="d-block">Research Interest 1, Research Interest 2</span>
        </div>
    </div>
</div>
```

Group sections are: PI, PhD Students, MS Students, Undergraduate Students, Alumni/Visiting.

### Citation Map

`citationmap.py` uses the external `citation_map` Python package (pip-installable) to regenerate `citation_map.html` from Google Scholar data. The scholar ID is hardcoded in the script (`9ajdZaEAAAAJ`). This page is auto-generated — edit the script rather than the HTML directly.

## Styling Notes

- Texas A&M maroon branding: `rgb(80, 0, 0)` / `#500000`
- Google Fonts: Cabin (body), B612 Mono (monospace)
- Responsive breakpoints via Bootstrap 4 grid
- Icons: Font Awesome (`fab fa-*`) for social links, Academicons (`ai ai-*`) for academic profiles (Google Scholar, ORCID)
