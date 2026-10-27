# CIIE manual Excel sync

Upload these files to the **root of the same GitHub Pages repository**:
- `index.html` (rename the supplied buyer dashboard HTML)
- `ciie-data.json`
- `scripts/update_excel.py`
- `.github/workflows/update-ciie-excel.yml`

GitHub repository → Settings → Secrets and variables → Actions → Variables → New repository variable:
- Name: `ONEDRIVE_DOWNLOAD_URL`
- Value: the anonymous OneDrive link that downloaded your XLSX in incognito, with `?download=1` (the script adds it if omitted).

Then GitHub → Actions → **Update CIIE Excel data (manual)** → Run workflow.
Check job logs for `OK: ...`. Wait for GitHub Pages deployment to finish. Reload the buyer dashboard or wait 10 seconds.

Important:
- This works only if GitHub-hosted runners can anonymously download the XLSX. If the response is an HTML login page, the workflow fails clearly; the OneDrive share link may need adjustment.
- GitHub Pages and the `ciie-data.json` file are PUBLIC. The script intentionally excludes buyer phone/email/WeChat and the raw Excel file. It DOES publish buyer code and name and survey status; if these are confidential, don't use public GitHub Pages for them.
- Existing meeting assignments are carried over from the prior JSON, matched by buyer code. If you change a buyer's code, their prior meeting assignments are not automatically moved. Excel does not contain an explicit meeting-assignment table.
- The published JSON is a snapshot updated ONLY when admin runs the workflow. The page checks for newly published JSON every 10 seconds; refreshing also loads the latest JSON.
- GitHub Pages does not provide secure authentication; 4-character buyer codes are convenience codes, not access control.
