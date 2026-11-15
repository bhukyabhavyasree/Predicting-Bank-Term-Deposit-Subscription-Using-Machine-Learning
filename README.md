# Predicting bank term-deposit subscription (ES 335 project)

Interactive project website (static HTML/CSS/JS on GitHub Pages) using the UCI *Bank Marketing* data.

| Required link | Value |
|---|---|
| Live GitHub Pages site | `https://<github-username>.github.io/<repo-name>/`  (fill in) |
| Source repository | `https://github.com/<github-username>/<repo-name>`  (public, or add the instructor/graders as collaborators) |
| Author(s) | [your name] (+ partner, if any) |

## Question and headline
Using only information available before a call, can we rank clients by their likelihood of subscribing to a term
deposit, and does the ranking hold on a later period? Chronological 60/20/20 split. Logistic regression reaches
test ROC-AUC 0.695 / PR-AUC 0.491, roughly tying the one-line rule "previous campaign succeeded" (0.628 / 0.480);
gradient boosting is lower (0.452 PR-AUC). The subscription rate drifts from 4.8% (train) to 30.8% (test).

## Where things are
- `analysis/run_analysis.py` - all modelling code (preprocessing, baselines, tuning, evaluation, errors). Writes every number the site shows.
- `docs/` - the website: `index.html`, `assets/style.css`, `assets/app.js`, `data/results.json` and `results.js`.
- `data/` - copy of `bank-additional-full.csv` and its documentation.
- `VIVA_NOTES.md` - key choices and likely "small change" questions.

## Data access
UCI Machine Learning Repository, "Bank Marketing" (`bank-additional.zip` -> `bank-additional-full.csv`),
https://doi.org/10.24432/C5K306, CC BY 4.0. No account, credentials or API key needed. A copy is in `data/`,
so nothing has to be downloaded. The data has no names or contact details.

## Setup / rebuild
```bash
python -m venv .venv && source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python analysis/run_analysis.py data/bank-additional-full.csv docs/data/results.json   # ~4 min, seed 42, deterministic
python -m http.server -d docs 8000                       # open http://localhost:8000
```
Split details: rows in file order; train = rows 0-24,711, validation = 24,712-32,949, test = 32,950-41,187.
Settings are chosen on validation (PR-AUC), models refit on train+validation, test scored once.
Tested with Python 3.13, numpy 2.5.3, pandas 3.0.5, scikit-learn 1.9.1.

## Publish on GitHub Pages
1. Create a repository and push this folder (keep `docs/` at the top level).
2. Settings -> Pages -> Build and deployment -> Deploy from a branch -> `main` / `/docs` -> Save.
3. After about a minute the site is live at the URL in the table above. Open it and check the charts and the explorer render.
4. Make the repo public (or add the instructor and graders), then record both links. In a pair, both partners confirm the same links.

## AI-use disclosure
I used Claude (Anthropic, via Claude Code) for brainstorming the design, writing and debugging the analysis script,
building the website code and charts, and drafting and editing text. Claude suggested leakage checks (excluding
`duration` and `campaign`). All reported numbers come from running `analysis/run_analysis.py`; re-running reproduces them.
[Add your own checks: what you re-ran or verified independently.]

## Citations
- Moro, S., Rita, P., Cortez, P. (2014). *Bank Marketing*. UCI Machine Learning Repository. https://doi.org/10.24432/C5K306 (CC BY 4.0).
- Moro, S., Cortez, P., Rita, P. (2014). A data-driven approach to predict the success of bank telemarketing. *Decision Support Systems* 62, 22-31.
- Pedregosa et al. (2011). Scikit-learn: Machine learning in Python. *JMLR* 12, 2825-2830. Also pandas and NumPy.
- Fonts: Archivo, Source Serif 4 (SIL OFL) via Google Fonts. Charts are hand-written SVG; no copied code.

## Before submitting
Replace `[your name]` here and in `docs/index.html`; fill in the two links above; add your own checks to the AI-use note
in both places; confirm the citation and licence details on the UCI page.
