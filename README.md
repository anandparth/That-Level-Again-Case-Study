# That Level Again — Case Study

**📖 Read it live:** [anandparth.github.io/That-Level-Again-Case-Study](https://anandparth.github.io/That-Level-Again-Case-Study/)

Case study of the troll platformer built into [parthanand.in](https://parthanand.in) — a game funded by the site's own coin economy, where **1 coin = 1 life**.

🎮 **Play it:** [parthanand.in/arcade](https://parthanand.in/arcade)

## The short version

- **84 single-screen stages** across 12 levels, each one **machine-proven beatable** — a beam-search solver plays the real engine and blocks the build if any stage (or any hidden key) is unreachable.
- **36 golden keys**, three per level, never in adjacent stages; all seven stages cleared *plus* all three keys unlocks the next level.
- An economy tuned against paywall math: deaths cost 1 ◉, clearing pays +5, opener stages retry free, and a broke player gets a pity retry instead of a wall.
- **41.6 KB engine, zero dependencies**, fixed 60 Hz deterministic simulation, 275+ automated checks before deploy.
- A secret ending nobody is told about.

## In this repo

- [`index.html`](index.html) — the case study itself: hand-drawn Excalidraw-style borders around real 8-bit game assets, zero dependencies
- [`CASE-STUDY-SPEC.md`](CASE-STUDY-SPEC.md) — the content (final copy) and the build plan for integrating it into the portfolio: data shapes, asset capture instructions, verification checklist, and the gotcha ledger from the original build.

Built solo in two days, August 2026. Mechanics studied from Level Devil (Unept); the name, all 84 layouts, and the art are original.
