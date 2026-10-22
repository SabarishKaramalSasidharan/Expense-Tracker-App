# Design Log

Source for all entries below: Claude Code working sessions with Sabarish (no external review docs or threads).

## Decisions

- 2026-10-22 — Monthly budget from Nov 2026 (on the ₹3,08,000 lowest salary), agreed by Sabarish in chat: EMIs ₹1,20,000; groceries ₹10,000; Swiggy ₹10,000; investment ₹28,500; gold chit ₹15,000; subscriptions ₹1,800; household help ₹22,900; family support ₹8,500; insurance RDs ₹23,860 (six policies, yearly premium ÷ 12, rounded up); maintenance RD ₹6,900 (₹3.50/sq ft × 1,915 sq ft × 3 months paid quarterly, plus lift AMC); other bills ₹9,500; leaves ₹51,040 for shopping, medical, fuel, miscellaneous. Credit card use stops. Why: the ₹39,504 maintenance payment on 2 Jun 2026 was a catch-up (Dec–Feb maintenance, corpus fund, lift AMC), not a monthly bill. OPEN: whether the corpus fund (₹17,235 for Dec–Feb) recurs quarterly; ₹5,745 a month if it does. NOT yet applied to the app's budget targets.
- 2026-10-22 — Statement import (Aug–Sep 2026): own-account transfers, loan repayments, the Morgan Stanley inflow, FD/RD closures, SIPs and salary are not imported as expenses. Credit card bills are logged as lump sums under "Credit card bill" (no card statements). Home loan EMIs (₹82,500 Bangalore + ₹37,600 Kerala) are logged on the 4th of each month from Sabarish's figures, not read from statements. Baby shower is a custom category. Why: avoids double-counting money moved between the household's accounts.
- 2026-10-22 — OPEN, not built: monthly analysis by pay cycle (salary credit date to the day before the next, e.g. 27 Aug–27 Sep) instead of calendar month. Salary landed 28 Jul, 27 Aug, 28 Sep.
- 2026-10-04 — Logo is a spending donut (green/amber/blue segments) with a white ₹ on the navy header gradient. Why: echoes the Home chart and the existing palette; there was no logo or home-screen icon before.
- 2026-10-04 — Home period controls (Day/Week/Month/Year + prev/next) sit above the summary, and the summary is one fixed-shape card for every period. Why: the old summary changed from 3 cards to 1 above the controls, so the controls jumped on every tap.
- 2026-10-04 — Unused budget rollover is opt-in (toggle on Home, stored in Firestore `settings/prefs`), envelope-style: carries unspent amounts forward from the first transaction month, overspend does not go negative. Why: avoids silently changing budget numbers.
- 2026-10-04 — Recurring expenses post automatically on their due day, starting from the next due date (not retroactively). Why: avoids duplicating an expense the user already entered by hand for the current month.
- 2026-10-04 — Transaction delete uses an undo toast instead of a confirm dialog. Recurring and goal deletes keep the confirm dialog.
- 2026-10-04 — Receipt photos not built. Why: needs Firebase Storage, which is not set up.
- 2026-10-03 — SMS auto-import dropped (user: "ignore the sms parse"). iOS has no API to read SMS; clipboard and share-sheet alternatives were not wanted.
- 2026-10 — Layout is a bottom nav (Home, center +, Transactions). Salary is entered per month and stored per month so past months keep their own value.

## Review feedback

- 2026-10-04 — Sabarish, chat: the ₹ in the logo is broken. Status: addressed (redrawn with a full bowl, two bars and a longer leg; the exact symptom was not described).
- 2026-10-04 — Sabarish, chat: Home period buttons are "a total mess", top and bottom change when switching. Status: addressed (commit 2157cbb).
- 2026-10-04 — Sabarish, chat: asked for competitor research and the missing best features/UX, then "do all the 9". Status: addressed (see Iterations). Research covered feature existence from marketing pages only; competitor UI layouts were not verified.
- 2026-10 — Sabarish, chat: bottom nav icons overflowing the bar. Status: addressed (commit 6744c3e).

## Iterations

- 2026-10-22 — Imported 121 transactions dated 1–22 Oct 2026 (₹4,53,449.32) into Firestore, tagged `stmt-import`, from the three HDFC statements (1–22 Oct) and the StanChart CSV. Skipped as already entered by hand: Nanny ₹22,000 (the ATM withdrawals), Money sent to dad ₹5,000, Car cleaning ₹900. EMIs ₹1,20,100 logged on 12 Oct, the day the money moved. Cloudnine ₹82,000 (8 Oct) logged as Medical; Murugesan V ₹10,000 (5 Oct) left in Miscellaneous. Open: ₹12,25,000 StanChart transfer on 17 Oct to an own account was excluded. Source: chat session, statements in `Aug - Oct 2026 _ Statements/`.
- 2026-10-22 — Imported 135 transactions dated 1 Aug–30 Sep 2026 (₹8,12,395.52) into Firestore, tagged `stmt-import`, from 5 bank statements. Source: chat session, statements in `Aug - Sep 2026 _ Statements/`.
- 2026-10-04 — Redrew the ₹ in the logo (`icon.svg`, header mark, regenerated `apple-touch-icon.png` and `icon-512.png`). The first version's bowl was too flat and the bars nearly merged.
- 2026-10-04 — Added logo: header mark, favicon (`icon.svg`), home-screen icon (`apple-touch-icon.png`), 512px `icon-512.png`.
- 2026-10-04 — Added: budget progress bars and "safe to spend per day"; comparison vs previous period (summary and per category); daily/monthly bar charts with tap-to-drill; Day view lists the day's biggest expenses; search and category/person/month filters; "added by" names and a "who spent" split; amount-first add form with recent-category chips and Today/Yesterday; recurring expenses; undo on delete; tags and notes; savings goals; optional budget rollover; last period choice remembered, tap label to jump to today, swipe to change period.
- 2026-10-04 — Fixed: Prev/Next on the 31st skipped months (month arithmetic now clamps the day); default dates used UTC and could be a day behind before 5:30am IST.
- 2026-10-04 — Home layout stabilised (commit 2157cbb).
