# WoW Collector's Edition Watch

Automated watcher for new listings on EB Games Australia matching a "world of warcraft" search:
https://www.ebgames.com.au/search?q=world+of+warcraft&sort=releasedate&order=desc

`snapshot.json` holds the page-1 result list from the most recent check (title/category/date/price, in order).
Each scheduled run compares the live page against this file — if the list has changed, it reports the new item(s)
found and commits the updated snapshot.

Note: EB Games' site sits behind Cloudflare bot protection. Plain HTTP fetches (e.g. WebFetch, curl) get a 403;
only a real JS-capable browser reliably gets through. This routine attempts `WebFetch` anyway since Cloudflare
behavior can vary per-request/IP — if it consistently fails, this approach needs to move to something with real
browser rendering (e.g. a self-hosted changedetection.io instance) instead.
