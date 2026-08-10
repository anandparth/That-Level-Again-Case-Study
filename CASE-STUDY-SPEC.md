# THAT LEVEL AGAIN — Case Study Build Spec

**Status:** SPEC ONLY — nothing integrated, nothing baked, nothing deployed.
**Written by:** Fable (planning agent), 2026-08-11, from the actual build session that shipped the game.
**For:** a Sonnet-class builder agent. Follow this document exactly. Every sentence of case-study copy in Part 2 is FINAL — do not rewrite, paraphrase, or "improve" it. Your job is integration, asset capture, and verification.
**The subject:** the game live at **https://parthanand.in/arcade** — a coins-as-lives troll platformer built into Parth Anand's portfolio, shipped 2026-08-10.

---

## PART 0 — Hard rules (violating any of these is a failed build)

1. **Never hand-edit `D:\Dev\portfolio\site\`.** Design sources live in `D:\Work\Claude\concepts\variants\`. Pipeline: edit variants → `npm run bake` → `npm run audit` (must exit 0) → commit → push. All from `D:\Dev\portfolio`.
2. **Never deploy.** `netlify deploy --prod --dir site` runs only on Parth's explicit word. Pushing to GitHub does NOT deploy (repo is not linked to Netlify CI). Stop after local verification and show Parth the preview.
3. **Email armour:** after every bake, `grep -rnI "parthanand1705@gmail.com\|@gmail.com\|wa.me\|mailto:" site/ --include=*.html --include=*.js --include=*.css` must find nothing. No phone/WhatsApp anywhere.
4. **Commits:** single-line messages, lowercase prefix style (`feat:`, `content:`, `docs:`), never credit an AI as co-author.
5. **Do not touch** `game-engine.js`, `game-levels.js`, or anything under `level-devil/`. The game is live and verified; this task is a case study ABOUT it.
6. **Locked pages** (home, about, work, case template, contact, playground, 404) change only where this spec says.
7. Every claim in the copy below is TRUE and was machine- or hand-verified in the build session. Do not add new numbers.

## Key facts (verified — cite these, nothing else)

| Fact | Value |
|---|---|
| Live URL | https://parthanand.in/arcade (secret ending: /reward — never advertise it) |
| Shipped | 2026-08-10, Netlify deploys `6a79da8d` → `6a79eb73` |
| Content | 12 levels × 7 stages = **84 stages**, **36 golden keys** (3/level, never in adjacent stages — 10 valid spreads) |
| Engine | **41.6 KB** hand-written JS, **0 dependencies**, fixed 60 Hz simulation, fully deterministic (no `Math.random`, no wall-clock in the sim) |
| Levels file | 34.8 KB of pure data — ASCII tilemaps + a trigger DSL |
| Economy | 1 coin = 1 life on the site-wide `pa-coins` wallet; first try free; door-opener stages retry free; +5 first clear, +15 level bonus, +25 key; 6-second pity retry at zero coins; one-time 10-coin stake |
| Verification | beam-search solver proves **84/84 stages beatable**; every key placement proven collectible; **275+ automated browser checks** across 7 Playwright suites; production smoke drives the real keyboard (42/42) |
| Solver catches | 2 of 3 hand-authored example levels in the plan were geometrically impossible; all 5 SPRINGS stages were unbeatable from one engine line (velocity zeroed after the spring fired); solver passed 6-4 via an inhuman line while the human route was impossible — Parth caught it by playing |
| Research base | Level Devil (Unept, 2023) — mechanics and "troll grammar" studied; name, all 84 layouts, and art are original |
| Art | door = stone arch drawn per-row in code; key sprite extracted from Parth's own art (7× upscale detected and reversed to a 56×50 sprite); player = small black pixel human drawn as rects |

---

## PART 1 — What this case study is

The sixth case study on parthanand.in, rendered by the existing template (`case.html` + `case-data.js`) — **zero template changes needed**; it is data-driven. Plus a seventh entry on the Work page. Same Excalidraw-plus-8-bit theme as everything else: paper `#fbfaf4`, ink `#222019`, Caveat hand-notes, Bricolage display, sketch borders, real game sprites as illustration.

Why it earns the slot: it is the only project with no NDA, full authorship, and **machine-verifiable claims** — the case study can say "every level is provably beatable" and mean it literally.

---

## PART 2 — THE CONTENT (final copy — paste verbatim)

Add this entry to `CASES` in `D:\Work\Claude\concepts\variants\case-data.js`, after `canon`:

```js
tla: {
  id: 'tla',
  lvl: 'SIDE QUEST · 2026',
  title: 'That Level Again — a game that lies to you',
  role: 'Designer · Engineer · Economy design · QA architecture',
  period: '2026 · parthanand.in — solo, two days',
  href: 'https://parthanand.in/arcade',
  hook: 'This site pays visitors in coins for exploring. Coins for what? I built the answer: a troll platformer where 1 coin = 1 life — and every one of its 84 stages is machine-proven beatable.',
  overview:
    'A pixel platformer living inside this portfolio, funded by its own coin wallet. Twelve levels, eighty-four single-screen stages, thirty-six hidden keys. The floor lies, the exit runs away, gravity is a preference. Built framework-free in a 41.6 KB deterministic engine, balanced so a broke player is never dead-ended, and shipped behind 275+ automated checks — including a search bot that plays the real engine and proves every stage has a solution.',
  challenge: [
    'The portfolio already had a coin economy — visitors earn ◉ for poking around — but nothing to spend it on. Dead currency is worse than no currency. The brief I set myself: make the coins matter with an arcade where 1 coin = 1 life, cloned from the feel of Level Devil, the viral troll platformer.',
    'Two traps hid inside that brief. First, the economics: a troll platformer kills you 3–8 times per stage by design, but a typical visitor arrives holding 10–40 coins — a literal 1:1 economy is a paywall wearing a game costume. Second, the content: 84 hand-authored stages is 84 chances to ship a level that cannot actually be finished, and a broken stage in a game about dying looks identical to a hard one.',
  ],
  insight: 'In a game built on lying to the player, the one thing that can never lie is the level itself — so I made solvability a compile step. A search bot plays the real engine and refuses the build if any stage, or any key, is unreachable.',
  mockups: [
    { img: 'tla-death', cap: 'the economy at the moment it bites — retry costs 1 ◉, door-openers stay free, broke players get a pity timer instead of a wall' },
    { img: 'tla-keystage', cap: 'a golden key stage — three per level, never adjacent, every placement machine-proven collectible' },
    { img: 'tla-reward', cap: 'finish everything and my avatar walks out to tell you a sequel is coming — the one page the site never advertises' },
  ],
  approach: [
    { t: 'deconstructed the troll grammar', d: 'Studied Level Devil the way you would a rival product: a 36-trap taxonomy grouped by which promise each trap breaks — the floor lies, the goal lies, the rules change. The design rule that fell out: every surprise must teach; a trap that kills you twice the same way is a bug.' },
    { t: 'did the economy math before the fun', d: 'Blind-run death rates (3–8 per stage) versus real wallet sizes (10–40 ◉) said a strict 1:1 economy stops most visitors inside two levels. So deaths cost 1 ◉ but clearing pays +5, opener stages retry free, and a zero-coin player gets a 6-second pity retry — the meter reads as tension, never as a toll booth.' },
    { t: 'built the engine to be interrogated', d: 'Fixed 60 Hz timestep, zero dependencies, and a simulation with no randomness and no wall-clock — same inputs, same result, every time. That is not purism; determinism is what makes a level provable.' },
    { t: 'made a bot earn the word "beatable"', d: 'A beam-search solver plays the actual engine — not a model of it — and must reach the door in every stage before anything ships. It caught two of my three example levels as geometrically impossible, and one engine line that silently made all five spring stages unwinnable.' },
    { t: 'let the human overrule the machine', d: 'The solver passed level 6-4 through a line no person would find while the intended route was impossible — Parth-the-player caught what the bot could not. Rule kept from that day: machine-proof solvability, human-check feel.' },
    { t: 'shipped it like a product, not a toy', d: 'Seven Playwright suites — economy paths, progression locks, page audit, whole-site gate — plus a production smoke test that plays stage one with a real keyboard on the live site: dies, retries free, clears, collects the bounty.' },
  ],
  solutions: [
    { t: 'a game the site can afford', d: 'The coin loop closed: earn ◉ anywhere on the site, spend it in the arcade, win it back by playing well. First try always free, so an empty wallet is never a locked door.' },
    { t: 'progression with real stakes', d: 'A level is seven stages; three hide golden keys, never in neighbouring stages. All seven cleared AND all three keys unlocks the next level — so keys are a reason to return, not decoration.' },
    { t: 'a secret worth keeping', d: 'Clearing all 84 stages with all 36 keys opens /reward — my walk-cycle avatar strolls in and reveals THAT LEVEL AGAIN 2. No menu links it, the sitemap omits it, and a CSS specificity bug that briefly leaked it to everyone became a fix and a lesson.' },
    { t: 'a QA harness as part of the design', d: 'Solvability as a compile step, key placement proven by replaying the winning path, 275+ checks green before deploy. The claim "every level is beatable" is not marketing copy — it is a test result.' },
  ],
  ba: {
    label: 'one door design, two tries',
    before: { img: 'tla-before', cap: 'variant B — a walkable corridor of doors; charming, rejected for feeling zoomed-in and slow to scan' },
    after: { img: 'tla-after', cap: 'the shipped title screen — two buttons, the coin rule in plain text, and the whole game one tap away' },
  },
  shots: [
    { img: 'tla-title', cap: 'the title screen — START resumes exactly where you owe a stage or a key' },
    { img: 'tla-select', cap: 'level select — locks, key counts and per-stage chips; gold means a key is still in there' },
    { img: 'tla-machines', cap: 'level 12, MACHINES — timed lasers, turrets and an advancing wall, all built from a 23-action trigger DSL' },
  ],
  loot: {
    stats: [
      { n: '84', label: 'stages, all machine-proven beatable' },
      { n: '36', label: 'keys, every placement verified' },
      { n: '275+', label: 'automated checks before deploy' },
      { n: '0', label: 'dependencies in a 41.6 KB engine' },
    ],
    meter: { label: 'stages the solver proves beatable', pct: 100, val: '84/84' },
    unlock: 'level architect — built a game where "every level works" is a test result, not a promise',
  },
},
```

**And append `'tla'` to ORDER:** `ORDER: ['cmp', 'fraud', 'okto', 'hmlc', 'canon', 'tla']` — this wires the next-quest cycle automatically.

> Builder note: `ba` is optional and already guarded — verified: `case.html` line ~290 wraps the whole block in `if (C.ba)` (the fraud entry ships without one). No template change needed.

---

## PART 3 — Asset production (7 webp files → `concepts/variants/assets/case/`)

All captures from the **local baked preview** (`npm run serve` in `D:\Dev\portfolio` → :5599) except `tla-before`, which needs the variants server (`node serve.mjs` in `concepts/variants` → :5495 serves the rejected corridor variant `arcadeb.html`). Use Playwright headless, `deviceScaleFactor: 2`, viewport 1440×900 for desktop shots. Convert PNG → webp (`npx sharp-cli -i in.png -o out.webp -q 82` or cwebp; match the ~60–200 KB weight of existing case images).

| File | How to capture |
|---|---|
| `tla-title.webp` | `:5599/arcade`, wait 2.8 s (intro settles), full-viewport shot |
| `tla-select.webp` | `:5599/arcade` → click `#selectBtn` → click first `.mrow` → wait 500 ms. For a richer shot, seed a mid-game save first (localStorage `pa-ld`: level 1 cleared with 2 keys — copy the fixture shape from `_arcade-progress.js`) so pips/keys show state |
| `tla-machines.webp` | `:5599/arcade?level=12-7`, wait 1.4 s (laser cycles visible), screenshot the `.screen` element only |
| `tla-death.webp` | `:5599/arcade?level=1-2`, hold ArrowRight ~2.6 s to die, wait 900 ms, screenshot `.screen` (shows RETRY — 1 ◉) |
| `tla-keystage.webp` | Seed plan `{"3":[0,2,4]}` in `pa-ld`, open `:5599/arcade?level=3-1`, wait 1 s, screenshot `.screen` — golden key visible in-world + "key in this stage" HUD chip |
| `tla-reward.webp` | `:5599/reward?preview=1`, wait ~6.5 s (walk-on + reveal complete), full-viewport shot |
| `tla-before.webp` | `:5495/` (arcadeb corridor variant), wait 1.7 s, screenshot the `.corridor` element |
| `tla-after.webp` | Same frame as `tla-title` but you may reuse the title capture cropped to the hero block — before/after should feel like the same crop discipline |

Sanity: every image must load on the baked case page with zero 404s (the audit will catch a miss).

---

## PART 4 — Work-page entry (seventh project)

In `D:\Work\Claude\concepts\variants\work-data.js`, append to `PROJECTS` (after papercade):

```js
{
  id: 'tla', lvl: 'SIDE QUEST · 2026', title: 'That Level Again — a game that lies to you',
  sub: 'live at /arcade · built into this site', tags: 'Game Design · Systems · Zero-dependency JS',
  blurb: 'A troll platformer funded by this site\u2019s own coins — 1 coin = 1 life. 84 stages, 36 keys, and a search bot that proves every level is beatable before it ships.',
  loot: '84/84 stages solver-proven · live now',
  metrics: [{ v: '84', l: 'stages, all proven beatable' }, { v: '36', l: 'keys, placements verified' }, { v: '0', l: 'dependencies · 41.6 KB engine' }],
  color: 'var(--d-gold)', fill: 'var(--f-gold)',
  href: 'case.html' + '?id=' + 'tla',
},
```

**Non-negotiable details:**
- The `href` must stay in **plain string-concat form** — the bake's LINKS rewriter only matches `href="X` and `'X'`; a backtick template dodges it and ships a dead link. (This exact bug shipped once.)
- `metrics` are `{v, l}` objects — the big animated stat cards. Never plain strings.
- Palette pair `--d-gold`/`--f-gold` is unused by the other six entries and matches the coin theme.
- Do NOT renumber any existing `lvl` tags; `SIDE QUEST` exists precisely to avoid that.
- The panel's uniform-height logic (`sizePanel()`) measures every entry automatically — no changes, but re-run the mobile crop check (Part 6) since a seventh tab changes wrap behaviour.
- Home page (`v4a.html`) has its own work-curtain copy of the projects UI reading the same `work-data.js` — verify the seventh entry renders there too, and that `.s-work .wrap { width: 100% }` still holds the panel steady across tabs.

---

## PART 5 — Standalone repo page (PHASE 2 — only if Parth asks)

This repo later gets a GitHub-Pages standalone version (like `jobhai-fraud-case-study`). If commissioned:
- Single `index.html`, no build step, no framework. GSAP from CDN is allowed (the site's pattern).
- Theme tokens (copy exactly): paper `#fbfaf4`, paper-2 `#f5f3e8`, dot `#e3decf`, ink `#222019`, muted `#74705f`, gold `#FFC402`/`#c4973f`; fonts Bricolage Grotesque (display 800), Caveat (hand), Spline Sans Mono (labels), Excalifont for sketch-headers (bundle the woff2 or fall back to Caveat).
- Excalidraw borders = the **double-stroke seeded-wobble SVG** technique: sample each box edge at 4–5 points, jitter ±2.4 px with a seeded PRNG, stroke the path TWICE at different seeds (second pass at 0.55 opacity). One pass looks like a mistake; two passes read as hand-drawn. A working `sketch()`/`wobble()` implementation exists in `concepts/variants/arcadeb.html` — lift it.
- 8-bit garnish from the real game: `LD.drawDoor` (load `game-engine.js`, call `LD.setSprite('key', img)` + `drawDoor` on small canvases), `assets/key.png`, walk frames from `assets/walk/`.
- Animation rules: every ScrollTrigger entrance uses `once: true` + `clearProps: 'transform,opacity'` (lazy-loaded images invalidate trigger positions — this bug has bitten three pages). Never `clearProps: 'all'` on anything with inline `display`. Respect `prefers-reduced-motion`.

## PART 6 — Verification checklist (all must pass before showing Parth)

```
cd D:\Dev\portfolio
npm run bake                # clean
npm run audit               # 12 pages, 0 findings — catches missing tla-*.webp, dead links, dev chips
grep -rnI "parthanand1705@gmail.com\|@gmail.com\|wa.me\|mailto:" site/ --include=*.html --include=*.js --include=*.css   # exit 1
npm run serve               # :5599
```
Then (probes live in `C:\Users\Parth\AppData\Roaming\npm\node_modules\`, all take a base URL):
1. `node _deploy-audit.js` — expect **81/81**. If it asserts case-page details, extend rather than weaken it.
2. `node _arcade-verify.js http://localhost:5599/arcade` — 48/48; `_arcade-econ` 19/19; `_arcade-progress` 22/22; `_game-audit` 22/22. **These must not change** — if one fails, you broke the game, revert.
3. `node _papercade-verify.js http://localhost:5599/work` — this suite asserts work-page entry structure and may assume SIX entries; update its expectations to seven, keep every other assertion.
4. Manual browser pass at 1440×900 AND 390×844 of `/case?id=tla`: zero console errors; no horizontal crop (check bounding right-edges, not scrollWidth — clipped ≠ fitting); all 8 images load; loot meter animates to 84/84; next-quest cycle from canon → tla → cmp.
5. Work page + home curtain: seventh tab renders, stats count up, uniform panel height holds, START opens the case study.
6. Commit (style per Part 0), push. **Add a runbook row** in `docs/DEPLOY-RUNBOOK.md` Design-lock history, `Deploy: PENDING`. **STOP — do not deploy.**

## PART 7 — Gotcha ledger (every one of these has actually bitten this site)

- `[hidden]` loses to any class-level `display:` — pages hiding sections by attribute need `[hidden]{display:none!important}`.
- The bake strips `<span class="tag-variant">…</span>` dev chips — new pages need one; content additions don't.
- `bake-site.mjs` injects `color-scheme: only light` — never design assuming dark auto-invert.
- `padding: X 0 Y` shorthand on an element that also carries `.wrap` zeroes the mobile gutters. Recurs constantly.
- Grid children need `min-width: 0` or inner `minmax(min(Npx,100%),1fr)` — min-content blowout crops phones invisibly to scrollWidth checks.
- Hover handlers on anything tappable must gate `matchMedia('(hover: none)')` per event, never cached.
- Case images are `assets/case/<name>.webp`, lazy-loaded — hence the `once:true + clearProps` rule above.
- If a probe fails, first ask whether the probe's fixture is wrong (it was, three times in the game build) before touching the product.

---

*End of spec. The copy in Part 2 is the case study. Build it exactly.*
