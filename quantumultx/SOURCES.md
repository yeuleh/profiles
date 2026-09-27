# QuantumultX rule sources

| File | Upstream | Snapshot | License |
|---|---|---|---|
| Filter/Guard/Advertising.list | blackmatrix7/ios_rule_script `rule/QuantumultX/AdvertisingLite/AdvertisingLite.list` | 2025-12-08 | GPL-2.0 (`Filter/Guard/LICENSE.blackmatrix7`, exact upstream copy) |
| Filter/Guard/Hijacking.list | blackmatrix7/ios_rule_script `rule/QuantumultX/Hijacking/Hijacking.list` | 2025-06-06 | GPL-2.0 (same file) |

Snapshots are static; re-vendor manually to update. Local modification date: 2026-09-27 (also disclosed in each list's header `LOCAL-MODIFIED` line; upstream `UPDATED` dates retained). See `LICENSE.blackmatrix7` for full redistribution terms.

Snapshot modifications:

- Advertising: full `Advertising.list` (~12 MB) skipped for size; `AdvertisingLite` (~38k rules) vendored. Policy token rewritten `AdvertisingLite` → `REJECT` (resource-level `force-policy` still overrides). Removed:
  - `HOST-KEYWORD,adservice` — overbroad keyword.
  - `HOST-KEYWORD,umeng`, `HOST-SUFFIX,mmstat.com` — would shadow Unbreak DIRECT exceptions (`msg.umeng.com`, `msg.umengcloud.com`, `log.mmstat.com`, `sycm.mmstat.com`).
  - `HOST,safebrowsing.g.applimg.com` — Apple's Google Safe Browsing proxy host; removed to avoid interfering with safe browsing lookups (not asserted as a confirmed blanket disable).
  - `HOST-SUFFIX,sentry.io` — error-reporting ingestion used by many legitimate apps.
  - `HOST,checkip.amazonaws.com` — public-IP lookup endpoint used by VPN/network checks.
  Header counts adjusted accordingly.
- Hijacking: strict superset of the previous list (verified by diff); policy token rewritten `Hijacking` → `REJECT` only.
- Privacy: intentionally NOT synced — upstream (39,936 rules) rejects `safebrowsing.googleapis.com`, which risks interfering with safe browsing; existing curated list kept.
- Rewrite/Block/AdvertisingPlus.conf: srk24 `bilibili_splash.js` rule removed (URL returns 404, checked 2026-09-27); stray hostname entry `m` removed. Remaining script URLs (yichahucha, blackmatrix7 gist, smzdm archive) verified HTTP 200 on 2026-09-27.
