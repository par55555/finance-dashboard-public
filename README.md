# Finance dashboards

Two Claude dashboards that sit on top of a Robinhood connection:

- **`homepage/`** — net worth across Robinhood (live), Fidelity (share counts priced live), a bank account (balance grown at its APY) and a 401(k) (balance moved by listed proxy funds). Shows allocation, top positions, biggest gains and losses, and every holding.
- **`market/`** — index and sector moves, the VIX, weekly news tagged with the holdings each story touches, Robinhood's daily movers and trending lists with analyst ratings, a live screen of large profitable companies that have sold off, and upcoming earnings for what you own.

Both are built on Claude's Dashboard artifact type: each page is plain HTML plus `dash.loader` / `dash.calc` / `dash.draw` scripts, reading datasets defined in `datasets.json`.

## How the data works

| Source | How it stays current |
| --- | --- |
| Robinhood accounts, positions, quotes, crypto, bank, card | Live calls on the viewer's own Robinhood connector, every time the page opens |
| Fidelity | A file of share counts; prices come from the live quotes |
| Bank savings | A file with balance, APY and date; grown daily at the APY |
| 401(k) | A file with balance per fund and a listed proxy (e.g. VOO); moved by the proxy's change |
| News | A file refreshed weekday mornings by a scheduled task (`scheduled-task/`) |

Everything the pages call on Robinhood is read-only (`get_*` tools and `preview_scan`, which saves nothing).

## Setting it up

1. Create a Dashboard artifact in Claude and write `datasets.json`'s entries as `datasets/<id>` documents.
2. Copy each `data/*.example.json` to a real file, fill in your own numbers, and attach it as the matching file dataset.
3. Save `index.html` as `files/index.html`.

## What's not in this repo

No account numbers, balances, holdings, logins or tokens. The `data/` folder only holds made-up examples, and `.gitignore` keeps real data files out.
