# Kubernetes: A Comprehensive Tutorial — GitHub Pages site

A static, multi-page site. Each chapter is its own HTML page, with a persistent
left-panel chapter menu on every page and previous/next navigation at the foot
of each chapter.

## Files
- `index.html` — landing/cover page with a chapter grid
- `NN-*.html` — one page per chapter (18 chapters)
- `styles.css` — shared stylesheet for every page
- `.nojekyll` — empty hidden file; disables Jekyll processing (see note below)
- `nojekyll.txt` — a VISIBLE backup copy (rename to `.nojekyll` if needed)
- `.github/workflows/deploy.yml` — optional automated deploy via GitHub Actions

---

## About `.nojekyll` — please read

`.nojekyll` is an empty, *hidden* file (its name starts with a dot). It is
genuinely included in the `.zip` and `.tar.gz` archives, BUT:

> macOS Archive Utility and Windows Explorer's built-in zip extractor **silently
> skip dotfiles when extracting**. So even though the file is in the archive, it
> may not appear on disk after you unzip. This is an extractor behaviour, not a
> packaging problem.

**Good news: this site does not need `.nojekyll` at all.** Jekyll only ignores
files/folders whose names start with an underscore (`_`), and this site has
none. It will publish correctly with or without the file.

If you still want it present, do any ONE of these inside the site folder:

```bash
# macOS / Linux
touch .nojekyll
# or rename the visible backup:
mv nojekyll.txt .nojekyll
```

```powershell
# Windows PowerShell
New-Item -ItemType File -Name ".nojekyll"
# or: Rename-Item nojekyll.txt .nojekyll
```

Once `.nojekyll` exists you can delete `nojekyll.txt` and `RENAME_TO_DOTFILE.txt`.

---

## Deploy to GitHub Pages

### Option A — serve from a branch folder (simplest, no dotfile needed)
1. Commit this folder to your repo (e.g. as `docs/` on the `main` branch).
2. Repo **Settings → Pages**.
3. **Build and deployment → Source = Deploy from a branch**.
4. **Branch = main**, **Folder = /docs**, then **Save**.
5. Live at `https://<user>.github.io/<repo>/` in a minute or two.

(`.nojekyll` is not required for this to work — see note above.)

### Option B — serve from the repository root
Move these files to the repo root, then set **Folder = / (root)** in Pages.

### Option C — automated deploy with GitHub Actions (creates `.nojekyll` for you)
1. Put the site files at the repository root, keeping `.github/workflows/deploy.yml`.
2. Repo **Settings → Pages → Source = GitHub Actions**.
3. Push to `main`. The workflow runs `touch .nojekyll` at build time and
   publishes the site — so you never have to handle the hidden file yourself.

---

## Notes
- Fully static — no build step required. Fonts load from Google Fonts.
- All links are relative, so it works under a project subpath (`/<repo>/`) as
  well as at a domain root.
- To edit content, change the chapter HTML files and re-commit.
