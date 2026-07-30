# Changelog

All notable changes to this project are documented here. Format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions follow
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] — 2026-07-30

### Changed
- v1.1.0 only fixed the illustration — the skill's actual instruction was still additive-only
  ("define every term on first use"), which is what produced bloated output in the first place.
  This release changes the mechanism, not just the example:
- **Rule one — substitute before you annotate.** Defining a term in place is now the fallback,
  not the default. If a clinical/research term is used once and the reader only needs the fact,
  say its plain meaning and drop the jargon word entirely. Keep the term, with a first-use
  clause, only when the reader needs to recognize the *word* again later.
- **Rule two — one clarification per sentence.** Stacking a parenthetical and an em-dash aside
  in the same sentence is banned outright — it raises parse difficulty independent of word
  count. Two things to clarify means two sentences, not one sentence carrying both.
- `Output shape` and `Keep / drop` updated to state both rules as concrete dos/don'ts.
  `What this skill must not do` gained a matching bullet.
- Worked example updated to demonstrate both mechanisms directly: one term substituted away
  entirely, one term kept and defined, split across two sentences instead of stacked into one.

## [1.1.0] — 2026-07-30

### Fixed
- The worked example's "after" was 4x the length of the "before" and invented facts that
  weren't in the original passage (an unrelated "not sure" bucket, a re-run recommendation) —
  it read as making explanations longer and harder, the opposite of the skill's purpose.
  Replaced with a tight example (~1.5x length) that only adds the short defining clauses.
- Added **Rule one** ("this makes it easier to read, not longer") and a **No new facts** bullet
  to `Output shape`, making explicit that elibme translates jargon in place — it does not add
  backstory, caveats, or context beyond what the original passage already said.

## [1.0.0] — 2026-07-30

First public release.

### Added
- `elibme` skill: calibrates explanations to an asymmetric reader profile — full technical
  density on software/AI/infra, plain first-use definitions on clinical and
  research-methodology terms, no cross-domain analogies.
- Claude Code plugin manifest and a one-plugin marketplace, so the repo installs via
  `/plugin marketplace add troopdegen/elibme`.
- `install.sh` with four targets — `claude`, `cursor`, `codex`, `agents` — plus `print` for
  every other harness. AGENTS.md targets write into a delimited block that updates in place
  and uninstalls cleanly.
- `dist/AGENTS.md` and `dist/elibme.mdc` — pre-built adapters for installing by copying a file
  instead of running the script. Generated from `SKILL.md` by `./install.sh --build`.
- CI: manifest validation, SKILL.md frontmatter checks, shellcheck, an install/uninstall
  round-trip across every target, and a gate that fails if `dist/` drifts from `SKILL.md`.

[1.2.0]: https://github.com/troopdegen/elibme/releases/tag/v1.2.0
[1.1.0]: https://github.com/troopdegen/elibme/releases/tag/v1.1.0
[1.0.0]: https://github.com/troopdegen/elibme/releases/tag/v1.0.0
