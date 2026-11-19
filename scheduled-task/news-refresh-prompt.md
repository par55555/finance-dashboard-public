# Scheduled task: refresh the news tile

Runs weekdays at 6:33 AM ET (`CRON_TZ=America/New_York 33 6 * * 1-5`). Replace `<MARKET_DASHBOARD_SLUG>` and the extra symbols with your own.

---

Refresh the "What's happening" news tile on the Market Trends dashboard (artifact slug `<MARKET_DASHBOARD_SLUG>`). Do only what is described here; change nothing else on the dashboard and take no action in any brokerage account.

1. Find what I hold, read-only: call the Robinhood connector's `get_accounts`, then `get_equity_positions` for each account, and collect the symbols. Add these symbols held elsewhere: `<SYMBOLS>`. If Robinhood is unavailable, continue without the holdings list.
2. Gather the past 1-3 days of news with web search. Pick 15-18 stories across exactly these categories: Politics, World, Markets, Tech, Society (at least 2 each). Prefer original reporting from established outlets. Use only URLs that appeared in search or fetch results.
3. Write each story in your own words: a headline under ~14 words and a 1-2 sentence summary. No long quotes. Keep political items factual and neutral. Set `related` to the tickers from step 1 that the story plausibly affects.
4. Save the stories as a JSON array named `news.json`, each item `{"id", "category", "date", "headline", "summary", "source", "url", "related"}`.
5. Upload it with `upload_asset` to the dashboard, then update `datasets/news` with the new `source` (`kind: "file"`, the upload's `url`, `name: "news.json"`, `format: "json"`), `updated` and `edit`.
6. Finish with a 3-line summary: stories per category, the biggest market-moving story, and which holdings appear most.
