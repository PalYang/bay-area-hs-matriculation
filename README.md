# Bay Area High Schools — T25 University Matriculation

Research dataset comparing Bay Area public and private high schools by their matriculation outcomes to U.S. News Top-25 National Universities, covering roughly the past five graduating classes.

## Files

- **`bay_area_public_high_schools.html`** — ~37 public/charter schools across San Francisco, Peninsula, South Bay, East Bay, and North Bay. Per-county tables with confidence-tagged rows.
- **`bay_area_private_high_schools.html`** — ~30 independent and Catholic schools, grouped by sub-region. Includes tuition, class size, and most common T25 destinations where published.
- **`methodology_and_review.md`** — T25 reference list, master roster of ~78 Bay Area high schools, methodology critique, decision framework, and a reviewer's audit of the two HTML files.

## How to view

Open the `.html` files directly in a browser — they are self-contained (inline CSS, no external assets).

## Important caveats — read before drawing conclusions

1. **Selection bias dominates.** The schools at the top of the matriculation tables (Harker, Castilleja, Mission San Jose, Lynbrook, Gunn, Paly) admit students who were already on a strong trajectory. Their outcomes reflect *who they enroll*, not necessarily *what they teach*.
2. **Data is partial.** Most public schools do not publish per-college matriculation counts. Private schools publish more, but often as cumulative multi-year lists or as "accepted to" rather than "matriculated to." Rows are tagged HIGH / MED / LOW / EST confidence.
3. **The Palo Alto teen-suicide cluster is documented.** Optimizing purely on matriculation points toward the highest-pressure schools. School culture, mental-health support, and fit matter alongside the numbers.
4. **"T25" is fuzzy.** Rankings shift year-over-year; the analysis uses the U.S. News Top-25 National Universities set roughly current as of 2024–2025. LACs are excluded.
5. **Geography skews the list.** Bay Area students disproportionately attend UC Berkeley, UCLA, and Stanford — high T25 share partly reflects in-state preference, not just school strength.

See `methodology_and_review.md` for the full critique and a recommended decision framework.

## Data sources

Each row in the HTML tables links to its primary source where one was found (school profile PDFs, counseling pages, district reports, Niche, U.S. News). Sources are cited inline rather than collected centrally so it is easy to verify any single number.
