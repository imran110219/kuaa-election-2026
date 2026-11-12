# KUAA Election 2026 Candidate Directory

A responsive, self-contained candidate directory. All candidate data is embedded in `index.html`, so the page works as a local file and on GitHub Pages without a build step or network request.

## Publish this site

From the repository folder, add and push the page and this README to the `main` branch:

```bash
git add index.html README.md
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
- Responsive layout for phones and desktop screens

Batch years are inferred from the first two digits of the listed student ID: `90`–`99` map to 1990–1999, and `00`–`89` map to 2000–2089.
