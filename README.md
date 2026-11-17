# KUAA Election 2026 Candidate Directory

A responsive candidate directory and election statistics dashboard. The site works on GitHub Pages and as local HTML files without a build step. Shared colors, typography, page width, headings, and navigation are defined in `site.css`; candidate portraits are stored in `public/candidates/`.

## Publish this site

From the repository folder, add and push the public pages, protected analysis copies, candidate data, portraits, and README to the `main` branch:

```bash
git add index.html results.html stats.html voters.html candidate.html manifesto-insights.html manifesto-themes.json candidates.json site.css README.md deepstateneverdies/ public/candidates/
git commit -m "Add KUAA candidate directory"
git push origin main
```

Then configure GitHub Pages:

1. Open the repository on GitHub and go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Choose **main** as the branch and **/(root)** as the folder, then click **Save**.
4. Check the Pages section or the repository’s **Actions** tab for deployment status.

The site URL for this repository is <https://imran110219.github.io/kuaa-election-2026/>.

## Directory features

- Candidate cards grouped by position
- Search by candidate name or student ID
- Filters for position, batch, discipline, and previous-election status
- Downloads the current results as an Excel-compatible CSV or a print-ready PDF
- Candidate-wise vote count dashboard at `results.html`, available by direct URL and grouped by position with seat-range context
- Candidate-list statistics by batch cohort, exact batch year, and discipline, with donut and bar charts
- Candidate profile pages and inline PDF manifestos for candidates with a published manifesto
- Manifesto Explorer with Bangla/English text search, candidate filters, and a clickable top-10 theme chart
- Responsive layout for phones and desktop screens

`candidates.json` is the single editable source for candidate records, including `voteCount`, photos, manifestos, slogans, and previous-election status. The HTML pages contain generated snapshots so they also work when opened directly as files. When candidate data changes, ask Codex to refresh the snapshots. On GitHub Pages, pages also fetch the JSON file so the canonical data is used. Candidate vote counts start at `0` and should be updated in `candidates.json` as candidate-wise counts are provided. Each `photo` field should point to an existing image under `public/candidates/`. Add a structured `manifesto` object only when a candidate has published one, with its title, introduction, and proposal text transcribed from the source document. Candidate cards link to the reusable `candidate.html?id=...` details page, where the manifesto is rendered in the site layout.

`manifesto-themes.json` is the separate, manually reviewed theme map used by `manifesto-insights.html`. It stores theme definitions and candidate IDs with indexes pointing back to the relevant manifesto sections or proposals in `candidates.json`; it does not duplicate names or manifesto text. Theme assignment is semantic and may be multi-label. Counts represent candidates whose reviewed manifesto addresses a theme, not raw word occurrences or endorsement. When a new manifesto is added, review it against the shared theme definitions, update the reviewed ID list and references, and ask Codex to refresh the explorer's embedded local snapshot. The page fetches both JSON sources on GitHub Pages and uses embedded snapshots when opened directly as a local HTML file.

Batch years are inferred from the first two digits of the listed student ID: `90`–`99` map to 1990–1999, and `00`–`89` map to 2000–2089.

Candidates who won a seat in the 2023 election results are marked with `previouslyElected: 2023`; the badge is omitted for everyone else. The winners were identified by comparing vote totals with the number of available seats for each position in `বেসরকারিফলাফল.pdf`. Maintain this property in `candidates.json` and regenerate the HTML snapshots afterward.

## Public pages and private analysis policy

The main `index.html`, `stats.html`, and `voters.html` are public pages. They do not show a password prompt or a campaign-slogan selector, including when opened with an old `?analysis=` query. Keep all slogan-based candidate and statistics analysis in the two protected copies only.

The protected copies are authored in `deepstateneverdies/index.html` and `deepstateneverdies/stats.html`. Both have the shared-campaign-slogan selector; selecting a slogan filters the directory or recalculates the statistics and updates the URL with an `analysis` code for a direct link. They are available at:

- `/deepstateneverdies/index.html`
- `/deepstateneverdies/stats.html`

The public voter-list dashboard is `voters.html`, published at `/voters.html`, with aggregate counts in `voter-stats.json`. The JSON contains no names, rolls, email addresses, or phone numbers. Rebuild it from the local `active-voter-list.xlsx` when that source is updated. The workbook contains voter contact details and is excluded by `.gitignore`; do not publish it. Batch cohorts are estimates from the first two digits of six-digit rolls; 34 non-six-digit rolls are excluded. Voter percentages are shares of listed records (or interpretable rolls for the cohort chart), not turnout rates. The source has no explicit batch-year field or eligible-member denominator.

For local preview, open the HTML files directly or run `python3 -m http.server 8000` from the repository root and open `http://localhost:8000/index.html`, `http://localhost:8000/results.html`, `http://localhost:8000/stats.html`, or `http://localhost:8000/voters.html`. The `.html` suffix is needed for a basic local static server.

The shared password is the plaintext `PRIVATE_PAGE_PASSWORD` constant in each protected page. This is a client-side visibility gate only; the password and candidate/group data are included in the downloaded page source, so it does not provide actual access control. Do not describe these pages as confidential or use this gate for sensitive information.
