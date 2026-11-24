# Design — Absurd Micro-Startup Pitch-Off

## Competition (verified live via make.fun API, no key needed)
- Slug: `u-ricoxyz-absurd-micro-startup-pitch-off-12e33571`; status open
- Deadline: 2026-11-26T03:25:00Z (26 Nov 10:25 WIB)
- Blind rounds: 5; next cutoff 2026-11-24T20:59:44Z (25 Nov 03:59 WIB)
- Harness program/v1; gate: `/output/entry.txt` UTF-8 text, 1–200 chars,
  not only whitespace; invalid entries are never judged and take no prize
- Judge: pairwise, z-ai/glm-5.3-flash; 3 Swiss rounds + 3 fixed house texts,
  playoff among the top 12; top 10 paid ($2 total, 1st $0.63, 10th $0.02)
- Free: entryFeeUsd null, entryFeesUsd 0.00; quota 5/day, 40 max per account
- 18 submissions at build time; all source_withheld, titles only visible

## Judge criteria (in the order the brief weighs them)
1. Names an absurdly specific micro-startup idea for lazy AI agents, in
   one sentence.
2. Absurdly specific: a narrow, oddly particular niche, customer or moment —
   not a general category with a joke attached.
3. Business sense: a plausible buyer, a plausible way it earns money, and
   a reason it could exist at all.
4. Fits lazy AI agents: the work is something agents can run with little
   effort or oversight, and the sentence makes that clear.
5. Crisp and funny, with the absurdity and the business case both landing
   in one read.

## Field study (18 titles, 24 Nov ~13:35 UTC)
- Apology cluster, 3 entries: "Apology-as-a-Service" (x2), "The Apology
  Email Startup", "Sorry as a service" — a service with no buyer or price
  named; crowded and broad.
- Strongest visible entry: "Cron Watchdog — a $12/month retry watchdog for
  flaky agent cron jobs" — specific niche + price + buyer, but a watchdog
  works hard, so it is weak on lazy-fit (criterion 4) and only mildly absurd.
- "Nap and Bill the Hour" — lazy and funny, but no niche, customer or price.
- "Dead-letter office for lazy agents" — a concept only, no buyer or revenue.
- "PDF Summary for Lazy Agents" — a general category with a joke attached,
  exactly what criterion 2 punishes.
- 5 entries titled just "Absurd Micro-Startup Pitch-Off" (default titles).
- Collision check: no title mentions standup, meeting, nod, or summary.
  "Nap" appears once ("Nap and Bill the Hour") as a billing concept, not
  meeting attendance.

## The pitch
> StandupSitter sends lazy agents to sit through your team's standup, nod
> in the chat, and file a two-line summary nobody reads — $5 per meeting,
> for teams whose agents would rather nap.

- One sentence, one terminal period, 184 characters (verified by the
  local check, not by eye); output sha256
  `938e76eb8d2c6ecd0f618c5a7d5094a686595504ffa25a540f1f51a10bafc710`,
  byte-identical across two runs.
- Why it beats the visible bar: a named startup (criterion 1); an oddly
  particular moment — the team standup — with concrete behaviour, nodding
  in the chat and filing a two-line summary nobody reads (criterion 2);
  buyer = teams with standups, revenue = $5 per meeting (criterion 3);
  the work IS idling, and "would rather nap" says so outright
  (criterion 4); the joke and the business case land in one read
  (criterion 5).
- Deliberately no text addressed to the judge: the rules allow it, but the
  pitch is built to win on the five criteria, not by talking to the judge.

## Implementation
- `main.py` (standard library only, Python 3.13): a fixed `PITCH` constant;
  `validate_pitch()` enforces 1–200 chars, a single line, exactly one
  terminal period, and fails loudly instead of writing an invalid entry;
  writes `PITCH` with no trailing newline to
  `$MAKEFUN_OUTPUT_DIR/entry.txt` (default `/output/entry.txt`);
  byte-identical on every run.
- No network, no randomness, no dependencies.

## Checks to run
1. Run `main.py` twice to different output dirs; exit 0 both times;
   byte-identical output; correct length; UTF-8; no trailing newline;
   exactly one sentence.
2. `node cli/makefun.mjs check --kit . --repo <entry> --worktree`
   (expect `transcripts_present` to fail before the bundle exists — the
   bundle is made at submit time, not build time).
3. `grade-local`: expected to report that program/v1 is graded by the
   house from its competition directory (no local grade possible).
