# EtchLab Website

Marketing site for EtchLab live laser-engraving events. Static HTML on GitHub Pages at https://etchlabdesign.com (repo `aryehw330-lgtm/EtchLabWebsite`, **public**, serves from `main`). No build step: edit the files, push, and it is live in a couple of minutes.

- Pages: `index.html` (home), `engravables.html` (items catalog), `watch.html`, `privacy.html`, `terms.html`.
- Match the existing look: copy styles and patterns from the page you are editing instead of inventing new ones.
- Big images and videos in `images/` are not tracked. Only add the ones a page actually uses.

## Never publish these (the repo is public)
- `proposal-builder.html`, `Files/`, `.internal/`: internal tools with supplier links, cost basis and payment handles. They are git-ignored. Never `git add -f` them, never copy their contents into a tracked file.
- Client agreements, finished proposal PDFs, phone screenshots of clients, anything with a client's personal details.
- Before every commit run `git status` and read the list. If any of the above appears, stop and unstage it.

## Workflow
- Both owners edit this repo at the same time. `git pull` before you start and again before you push.
- Test at phone width (375px) before pushing. Check the nav, the items grid and the hero.
- Commit straight to `main` with a clear message. Never force-push or rewrite history. A mistake can always be undone with `git revert`.
- Local preview: `python3 -m http.server 8743 --bind 127.0.0.1` in this folder (local only, never the whole network), then open http://localhost:8743.

## Items catalog (`engravables.html`)
- Cards are `<div data-item-card data-cat data-name data-num data-search>`, grouped in `<div data-section="Jewelry|Leather|Metal|Wood|Tech|Judaica|Accessories">`. Copy an existing card for the exact markup.
- Photo goes in `images/items/<number>.jpg`. Use a square image; put non-square photos on a white (or blurred) square so the grid does not crop badly.
- Item numbers continue from the highest existing number. Search the file for the last one before assigning.
- After adding cards, update the static section counts and the total by hand.
- Do not flag lookalike items as duplicates when the color or photo differs; both are wanted. An item already on the site that a new proposal prices only needs its price updated.
- The public site shows no prices and no costs.

## Proposals, invoices and the proposal builder
These tools are private and live in a separate private repo, `aryehw330-lgtm/EtchLabInternal`.
- If `.internal/` exists in this folder, read `.internal/CLAUDE.md` and follow it. It covers the builder, the PDF generator and how new items are added to all the places they go.
- If it does not exist, set it up: `git clone https://github.com/aryehw330-lgtm/EtchLabInternal.git .internal && bash .internal/install.sh`.
- Always make proposals and invoices with `Files/proposal-generator/make_proposal.py` (dark format, new logo). Do not build PDFs any other way.
- Do not commit anything from those tools to this public repo.

## Known issue to keep in mind
`EtchLab-Items-Sheet.csv` is tracked here and served publicly, but it has costs and supplier links. The owner knows and has decided to leave it public. Keep updating it as `.internal/CLAUDE.md` describes, don't bring it up again, never link to it from a page, and ask the owner before moving, renaming or restructuring it.
