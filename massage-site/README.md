# Reimplement WordPress site as a static GitHub Pages site

This repository contains a saved copy of a WordPress site in the `target/` folder. The goal is to publish that site as a static website using GitHub Pages (serve from the `docs/` folder on branch `main`).

Files added:
- `scripts/copy-target-to-docs.ps1` - PowerShell script that copies `target/` into `docs/`, renames the main `.html` to `index.html`, and creates `.nojekyll`.

Quick steps

1. From the `massage-site` folder run the copy script in PowerShell (Windows PowerShell v5.1):

```powershell
.
\scripts\copy-target-to-docs.ps1
```

2. Review the generated `docs/` folder. If everything looks good, commit and push the changes to `main`:

```powershell
git add docs scripts/README.md
git commit -m "Publish static site to docs/ for GitHub Pages"
git push origin main
```

3. In the GitHub repository settings, enable GitHub Pages and set the source to:
- Branch: `main`
- Folder: `/docs`

4. (Optional) Preview locally before pushing:

If you have Python 3 installed you can preview the `docs` folder on localhost:

```powershell
cd docs
python -m http.server 8000
# open http://localhost:8000 in your browser
```

Notes and caveats
- The script performs a straightforward copy of the `target` folder. Some WordPress features (server-side PHP, forms, search, dynamic comments) won't work as-is and may need replacement or removal.
- External embedded widgets (booking iframes, third-party scripts) will continue to load from their original URLs as long as the external services allow it.
- If some asset paths are absolute (point to the original domain), you may want to rewrite them to relative paths. I can add a script to rewrite common patterns if you want.

If you'd like, I can:
- Run the script here and commit the `docs/` folder for you.
- Convert absolute URLs to relative ones.
- Add a small CI action to automatically build/publish on push.
