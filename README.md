# KUAA Election 2026 Candidate Directory

A responsive candidate directory and election statistics dashboard. The directory works as a local file and on GitHub Pages without a build step; candidate portraits are stored in `public/candidates/`.

## Publish this site

From the repository folder, add and push the public pages, protected analysis copies, candidate data, portraits, and README to the `main` branch:

```bash
git add index.html stats.html candidate.html candidates.json README.md deepstateneverdies/ public/candidates/
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
- Filters for position, batch, and discipline
- Downloads the current results as an Excel-compatible CSV or a print-ready PDF
- Candidate-list statistics by batch cohort, exact batch year, and discipline, with donut and bar charts
- Candidate profile pages and inline PDF manifestos for candidates with a published manifesto
- Responsive layout for phones and desktop screens

Candidate counts show representation on the final list, not voter turnout. The statistics page reads `candidates.json` when served from the site and includes an embedded copy as a fallback for direct `file://` viewing. Keep candidate records in `candidates.json` synchronized with the embedded fallbacks in `index.html`, `stats.html`, and `candidate.html` after changing candidate records. Each `photo` field should point to an existing image under `public/candidates/`. Add a structured `manifesto` object only when a candidate has published one, with its title, introduction, and proposal text transcribed from the source document. Keep it synchronized in `candidates.json` and the embedded fallbacks in all three HTML pages. Candidate cards then show a link to the reusable `candidate.html?id=...` details page, where the manifesto is rendered in the site layout.

Batch years are inferred from the first two digits of the listed student ID: `90`–`99` map to 1990–1999, and `00`–`89` map to 2000–2089.

## Public pages and private analysis policy

The main `index.html`, `stats.html`, and `voters.html` are public pages. They do not show a password prompt or a campaign-slogan selector, including when opened with an old `?analysis=` query. Keep all slogan-based candidate and statistics analysis in the two protected copies only.

The protected copies are authored in `deepstateneverdies/index.html` and `deepstateneverdies/stats.html`. Both have the shared-campaign-slogan selector; selecting a slogan filters the directory or recalculates the statistics and updates the URL with an `analysis` code for a direct link. GitHub Pages uses their Jekyll permalinks to publish them at:

- `/deepstateneverdies/index`
- `/deepstateneverdies/stats`

The public voter-list dashboard is `voters.html`, published at `/voters`, with aggregate counts in `voter-stats.json`. The JSON contains no names, rolls, email addresses, or phone numbers. Rebuild it from the local `active-voter-list.xlsx` when that source is updated. The workbook contains voter contact details and is excluded by `.gitignore`; do not publish it. Batch cohorts are estimates from the first two digits of six-digit rolls; 34 non-six-digit rolls are excluded. Voter percentages are shares of listed records (or interpretable rolls for the cohort chart), not turnout rates. The source has no explicit batch-year field or eligible-member denominator.

For local preview, run `python3 -m http.server 8000` from the repository root and open `http://localhost:8000/index.html`, `http://localhost:8000/stats.html`, or `http://localhost:8000/voters.html`. The `.html` suffix is needed for a basic local static server.

The shared password is the plaintext `PRIVATE_PAGE_PASSWORD` constant in each protected page. This is a client-side visibility gate only; the password and candidate/group data are included in the downloaded page source, so it does not provide actual access control. Do not describe these pages as confidential or use this gate for sensitive information.
