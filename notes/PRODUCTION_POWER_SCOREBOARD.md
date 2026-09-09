# Production power scoreboard

_Top 10 indie · gravity Newdrop_ · Policy: [TOP10_PRODUCTION_POWER.md](TOP10_PRODUCTION_POWER.md)

Refresh: `python3 scripts/production_power_scoreboard.py --write`

## Current snapshot (2026-09-09 07:20 UTC)

| Metric | Value |
|--------|------:|
| Newdrop merges (7d) | 20 |
| Non-noop cycles/day | 18 today · proj 58.9/day · week_avg 13.5 (bar ≥8) [PASS] |
| Free-desktop agent cap | 8 |
| Theater Active share | 0% (0/2 open) |
| Brain / daemons | CLEAN peer-loop=active improve-loop=active ssh_rc=0 |

Merges: #333 Feed CORS Expose-Headers nosniff + Content-Language (after # (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/333); #332 Crawl-brief canonical query 308 (after #331) (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/332); #331 Crawl-brief CORS Expose-Headers nosniff + Content-Language ( (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/331); #329 Public widget CORS Expose-Headers nosniff + Content-Language (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/329); #327 GitHub App install capability-URL noindex (after #325) (https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/327)

## Week log

### Week of 2026-09-01 → 2026-09-07 (baseline → cadence land)

| Metric | Value | Notes |
|--------|------:|-------|
| Newdrop merges (7d) | **3** | PRs [#16](https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/16), [#17](https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/17), [#18](https://github.com/heyitsmeyourbudlol-lgtm/caas-changelog/pull/18) |
| Non-noop cycles/day | recovering | CLEAN brain live; free-desktop cap 8 |
| Brain | CLEAN | mac-offloaded; meter credits CLEAN |
| Theater Active share | **0%** | Top10 Active = Newdrop-only open lines |
| Free-desktop agent cap | **8** | measured free concurrent (was phantom 96) |

**Verdict:** Merge bar hit (≥3). Cycles/day still the gap for a full green week. Streak clock: partial week; full green weeks start when cycles≥8 + merges≥3.

### Week of 2026-09-08 → 2026-09-14 (in progress)

| Metric | Value | Notes |
|--------|------:|-------|
| Newdrop merges (7d) | 12 rolling | Keep ≥3 |
| Non-noop cycles/day | **PASS** | T10-04 closed 04:45Z: **9 today · proj 45.4/day · week_avg 9.0** `meets_bar=true`; CLEAN side=hist=live=9 after brain-path rehydrate |
| Brain | CLEAN | peer+improve **active**; Mac LAs off |
| Cap | 8 | `max_parallel_agent_procs` |


## T10-04 evidence (2026-09-08)

Raise CLEAN non-noop cadence; keep free-desktop **cap=8**; NO PAY; Mac peer/improve LaunchAgents **not** enabled.

| Check | Result |
|-------|--------|
| BEFORE throughput | **5.0 cycles/h** · **4.0 non-noop/h** · rate 80% · window 5 |
| AFTER throughput | **4.0 cycles/h** · **4.0 non-noop/h** · rate **100%** · window 4 (post-wake; no SIGUSR1) |
| Day rollup (scoreboard) | **9 today** · **proj 45.0/day** · week_avg 9.0 · 04:47Z restamp (bar ≥8) **[PASS]** |
| CLEAN meters | **hist=9 · side=9 · live=9** after brain-path hist-rehydrate (was side=2 lag); reconfirm SSH 04:48Z |
| Close gate | Confirmed CLEAN side≥8 + `meets_bar=true` — **not** Mac sidecar (local side≈4 ignored) |
| peer-loop | **active** (USR1 trap proven — kill -s USR1 leaves active) |
| improve-loop | **active** (wake via `peer-turn.signal` — never `systemctl kill -s USR1`) |
| Anti-flap | sidecar `non_noop_by_day.json` · thin-save max-merge · dgx skip restart-if-active |
| `peer-turn.signal` | touched UTC wake |
| Cap | `max_parallel_agent_procs=8` · `free_desktop_agent_cap=8` |
| Mac | `mac-offloaded` present · peer/improve LaunchAgents absent |

**Note:** Countable day rollup excludes `local_only` + `deferred` verify ticks. SIGUSR1 / hard restarts used to wipe short `cycle_history` — durable `non_noop_by_day` + sidecar now survive flaps. Mac scoreboard must not false-PASS on hist-only while CLEAN sidecar lags — close only when CLEAN side≥8 or honest reconcile is documented.
## How to count a “meaningful” merge

User-visible or verify-backed (`npm test` / `check:controls`) change on Newdrop. Hub needles do not count.
