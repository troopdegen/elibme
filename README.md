# elibme

*Elibme* — explain like I'm a Biomedical Engineer — is what you say when an explanation either
talks down to you on the tech side or assumes fluency you don't have on the clinical/research
side.

This is a skill that calibrates an AI agent's explanations to one specific asymmetric reader
profile: deep fluency in software/infra/AI, but rusty on clinical terminology and new to
scientific-research methodology. It is not ELI5 — the tech register gets zero simplification.
It is not the agent's default density either — clinical and research-methodology terms get a
plain-language definition the first time they appear, with no cross-domain analogy standing in
for the real explanation.

**The one failure mode this skill exists to prevent:** explaining a clinical concept through a
software metaphor, or a research-methodology concept through a tech one. A wrong or strained
analogy teaches the wrong thing, and forces the reader to do a translation step even when it
lands right. The fix is not a metaphor — it's naming the unfamiliar term in one plain clause and
moving on.

## What it looks like

**Before (too dense — assumes research-methodology fluency):**
> The joint-count finding used N=62 as its denominator, but DECISIONS #58's census is N=64 —
> a cohort mismatch between the LLM's disease_variant classification and the ground-truth
> table-structure parse.

**After (elibme):**
> The 82% joint-count finding was measured against 62 notes — but a more careful earlier count
> (DECISIONS #58, done by directly reading each Word document's table structure rather than
> asking a model to classify it) puts the true number of RA notes at 64. The 62 came from the
> model's own guess during this week's sweep, which also produced a 9-note "not sure" bucket
> that shouldn't exist if the classification were perfect. So the joint-count percentage was
> computed over a slightly wrong group size, and should be re-run against the confirmed 64
> before it's cited formally.

Same information, same numbers, no analogy — the only change is naming what a "cohort" and a
"ground-truth count" are, once, in plain terms, instead of assuming the reader already tracks
that vocabulary.

## Install

The skill is one file — [`skills/elibme/SKILL.md`](skills/elibme/SKILL.md) — written as plain
Markdown with no harness-specific syntax in the body. Every install path below puts that same
body somewhere your agent reads, rewriting nothing but the frontmatter. Pick the one that
matches your tool.

### Claude Code

```
/plugin marketplace add troopdegen/elibme
/plugin install elibme@elibme
```

`/plugin update elibme` picks up later releases.

Or install it as a plain skill, without the plugin system:

```bash
git clone https://github.com/troopdegen/elibme.git
cd elibme
./install.sh
```

That writes `~/.claude/skills/elibme/SKILL.md`. Start a new session afterwards — Claude Code
does not pick up newly installed skills mid-session.

### Codex, Gemini CLI, Copilot, Zed, Aider, Windsurf, Jules

These read [AGENTS.md](https://agents.md). Run from your project root:

```bash
./install.sh --target agents      # ./AGENTS.md
./install.sh --target codex       # ~/.codex/AGENTS.md, global for Codex CLI
```

Both write into a block delimited by HTML comments, so the rest of your `AGENTS.md` is left
alone. Re-running updates that block in place instead of appending a second copy, and
`--uninstall` removes exactly that block.

### Cursor

```bash
./install.sh --target cursor      # ./.cursor/rules/elibme.mdc
```

Installed with `alwaysApply: false` and the skill's description in the frontmatter, so Cursor
pulls it in when it's relevant rather than on every turn. Reference it directly with `@elibme`.

### Without running anything

[`dist/`](dist) holds the same adapters pre-built, for copying by hand:

- [`dist/AGENTS.md`](dist/AGENTS.md) — paste into your project's `AGENTS.md`, or use it as one
  if you don't have it yet. It keeps the same comment delimiters `install.sh` uses, so you can
  hand it over to the script later and `--uninstall` will still find it.
- [`dist/elibme.mdc`](dist/elibme.mdc) — drop into `.cursor/rules/`.

These are generated from `SKILL.md`, byte-identical to what `install.sh` writes, and CI fails if
they drift. Regenerate with `./install.sh --build`.

For anything else — a system prompt, a custom GPT, a rules file with its own format:

```bash
./install.sh --target print
```

Writes the harness-agnostic body to stdout, no frontmatter, no markers.

### Uninstall

`./install.sh --target <same-target> --uninstall`. It only removes what it installed: each
target leaves a marker (a `.elibme-managed` file, or the comment delimiters) and refuses to
touch anything it did not write.

## Layout

```
skills/elibme/SKILL.md    the skill — the only copy of the content
dist/AGENTS.md            generated adapter, for AGENTS.md-family harnesses
dist/elibme.mdc           generated adapter, for Cursor
.claude-plugin/           plugin + marketplace manifests
install.sh                adapters over SKILL.md, and --build for dist/
```

Nothing that an agent auto-loads lives at the repo root — no `AGENTS.md`, no `CLAUDE.md`, no
`SKILL.md`. Those paths belong to *your* project, not to a repo you cloned to install something.
A root `AGENTS.md` here would be picked up by any agent you pointed at this clone, and would
collide with `./install.sh --target agents` if you ran it from the wrong directory. The
distributable copy lives in `dist/` instead, where it is inert until you move it.

## Using it

Say **"elibme"** — or "explain like I'm a BME", "more professional than eli5 but not as dense as
usual" — at any explanation. In Claude Code, `/elibme` invokes it directly.

It also fires on its own before a reply that's about to lean on undefined clinical or
research-methodology jargon, or reach for an analogy that crosses from one domain into the
other. It rewrites the sentence before sending, rather than appending a glossary afterward.

**It deliberately stays out of the way of tech/AI/infra content** — that register gets no
simplification, ever. This skill closes one specific gap: the unfamiliar 20%, named plainly,
without flattening the familiar 80%.

It composes with `mucho-texto`: that skill decides what's worth saying, this one decides how to
say the parts that cross into clinical/research territory.

## Provenance

Written after a real session in which the same explanation talked down on the tech side and
assumed fluency it shouldn't have on the clinical side — a cross-domain analogy is what tripped
it up. That worked example is preserved in the skill itself, because it's the failure it most
needs to avoid.

## License

MIT — see [LICENSE](LICENSE).
