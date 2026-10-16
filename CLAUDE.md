# CLAUDE.md — Collimator + spatial filter calculator

## What this project is
A single-page web calculator for a laser beam collimator with a pinhole spatial filter
(Keplerian telescope: laser → L1 → pinhole → L2). The user works on a synchrotron beamline
and uses this to design a red-laser collimator (default: 633 nm, f1 = 50 mm, f2 = 120 mm, pinhole 100 µm).

The UI has a Thai / English toggle, a live optical layout (SVG), a beam-size-vs-distance chart,
equations with substituted values, and an "export as SVG" button.

## Files
- `index.html` — the entire app: HTML + CSS + JS in one file. No build step, no dependencies
  except Google Fonts (IBM Plex Sans Thai).
- `README.md` — repo description. Contains the placeholder `YOUR-USERNAME` in the Pages link.
- `CLAUDE.md` — this file.

## Task: publish to GitHub Pages
1. Check that `git` and the GitHub CLI (`gh`) are installed and that `gh auth status` is logged in.
   If not logged in, ask the user to run `gh auth login` themselves (browser flow).
   Never ask the user to paste a password or token into the chat.
2. Replace `YOUR-USERNAME` in `README.md` with the GitHub username from `gh api user --jq .login`.
3. Initialise git, commit `index.html`, `README.md` and `CLAUDE.md` on branch `main`.
4. Create a **public** repo named `collimator-calculator` and push:
   `gh repo create collimator-calculator --public --source=. --remote=origin --push`
   If the name is taken, ask the user for another name (and update README.md to match).
5. Enable GitHub Pages from `main` / root:
   `gh api -X POST repos/{owner}/collimator-calculator/pages -f "source[branch]=main" -f "source[path]=/"`
6. Wait for the first build (`gh api repos/{owner}/collimator-calculator/pages/builds/latest`),
   then give the user the link: `https://<username>.github.io/collimator-calculator/`

## Rules when editing index.html
- Keep it one self-contained file; do not add a framework or build tooling.
- Every user-visible string lives in the `S` object with both `th` and `en` keys. Add new text to both.
- Physics lives in `calc(p)`. Model: Gaussian beam with M² scaling, 1/e² diameters, output waist at L2.
  - focal spot 2w_f = 4·M²·λ·f1 / (π·D_in)
  - pinhole transmission T = 1 − exp(−2a²/w_f²); recommended pinhole ≈ 1.57 × focal spot
  - D_out = D_in · f2/f1; z_R = π(D_out/2)² / (M²λ); collimated range ≈ 2·z_R
  - L2 / pinhole axial tolerance ≈ π·w_f² / (M²λ)
- SVG export: `exportSVG()` uses fixed hex colours (CX) so the file looks right outside the page.
  The save button uses Claude's `downloads` capability when available and otherwise falls back
  to a normal browser Blob download (the path used on GitHub Pages). Keep both paths.
- Test after changes: open `index.html` in a browser, switch languages, move each slider,
  and save an SVG in both languages.
