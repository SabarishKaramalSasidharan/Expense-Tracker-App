# Design Log

Source for all entries below: Claude Code working sessions with Sabarish (no external review docs or threads).

## Decisions

- 2026-10-04 — Logo is a spending donut (green/amber/blue segments) with a white ₹ on the navy header gradient. Why: echoes the Home chart and the existing palette; there was no logo or home-screen icon before.
- 2026-10-04 — Home period controls (Day/Week/Month/Year + prev/next) sit above the summary, and the summary is one fixed-shape card for every period. Why: the old summary changed from 3 cards to 1 above the controls, so the controls jumped on every tap.
- 2026-10-04 — Unused budget rollover is opt-in (toggle on Home, stored in Firestore `settings/prefs`), envelope-style: carries unspent amounts forward from the first transaction month, overspend does not go negative. Why: avoids silently changing budget numbers.
- 2026-10-04 — Recurring expenses post automatically on their due day, starting from the next due date (not retroactively). Why: avoids duplicating an expense the user already entered by hand for the current month.
- 2026-10-04 — Transaction delete uses an undo toast instead of a confirm dialog. Recurring and goal deletes keep the confirm dialog.
- 2026-10-04 — Receipt photos not built. Why: needs Firebase Storage, which is not set up.
- 2026-10-03 — SMS auto-import dropped (user: "ignore the sms parse"). iOS has no API to read SMS; clipboard and share-sheet alternatives were not wanted.
- 2026-10 — Layout is a bottom nav (Home, center +, Transactions). Salary is entered per month and stored per month so past months keep their own value.

## Review feedback

- 2026-10-04 — Sabarish, chat: Home period buttons are "a total mess", top and bottom change when switching. Status: addressed (commit 2157cbb).
- 2026-10-04 — Sabarish, chat: asked for competitor research and the missing best features/UX, then "do all the 9". Status: addressed (see Iterations). Research covered feature existence from marketing pages only; competitor UI layouts were not verified.
- 2026-10 — Sabarish, chat: bottom nav icons overflowing the bar. Status: addressed (commit 6744c3e).

## Iterations

- 2026-10-04 — Added logo: header mark, favicon (`icon.svg`), home-screen icon (`apple-touch-icon.png`), 512px `icon-512.png`.
- 2026-10-04 — Added: budget progress bars and "safe to spend per day"; comparison vs previous period (summary and per category); daily/monthly bar charts with tap-to-drill; Day view lists the day's biggest expenses; search and category/person/month filters; "added by" names and a "who spent" split; amount-first add form with recent-category chips and Today/Yesterday; recurring expenses; undo on delete; tags and notes; savings goals; optional budget rollover; last period choice remembered, tap label to jump to today, swipe to change period.
- 2026-10-04 — Fixed: Prev/Next on the 31st skipped months (month arithmetic now clamps the day); default dates used UTC and could be a day behind before 5:30am IST.
- 2026-10-04 — Home layout stabilised (commit 2157cbb).
