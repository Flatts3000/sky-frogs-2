# CLAUDE.md

Guidance for Claude Code working in this repo.

## What this is

**Sky Frogs 2** is the MC 26.x sequel to [Sky Frogs](../sky-frogs), built around
[Productive Frogs 2.x](../productive-frogs). It is **scaffolding, pre-alpha, and
not playable**. Nothing here has shipped and nothing here has a CurseForge
project yet.

This is a **separate repo, not a branch**, because Sky Frogs 1 is live and still
being patched (v1.6.2, 2026-08-09) and will be its own CurseForge project with
its own release pipeline. The two packs share a lineage, not a codebase.

### The authority for design

[`docs/decisions.md`](./docs/decisions.md) is the **settled decision log**. It is
the only file you may build against. Everything in it is decided; when it
conflicts with anything else, it wins.

Two supporting documents, neither of which is a build list:

- [`docs/sf1_retrospective.md`](./docs/sf1_retrospective.md) - the evidence base,
  distilled from the full SF1 community Discord export (3,216 human messages, 430
  participants, 2026-06-06 to 2026-08-07). Findings, not instructions.
- [`docs/player_feedback.md`](./docs/player_feedback.md) - one player's input,
  **held**. Captured so it is not lost; not a plan.

**Do not invent design.** If a thing is not in `decisions.md`, it is not decided,
and the correct move is to say so rather than pick something plausible. The
decision log's own "Open questions" and "Blockers" sections are the live list of
what is genuinely undecided.

### What is settled so far

| | Decision |
|---|---|
| D-1 | Slime Milk and Mob Slurry never run dry. Bountiful + Endless catalysts disabled; Rapid + Teeming stay. |
| D-2 | Cave Slimes do not spawn in a dark room. The pack adds nothing to natural spawning. |
| D-3 | Slime balls come from sieving dirt on the Builders' Sieve (0.25, string mesh). Resolves D-2. |

## Versioning targets

- Minecraft: **26.1.2**. Not 26.2 - KubeJS and FTB Quests have no 26.2 build, and
  Productive Frogs 2.x targets 26.1.2. 26.1.2 is the only version the whole stack
  shares.
- Loader: **NeoForge 26.1.2.94** (latest 26.1.2.x as of 2026-08-10).
- Java: **25**.
- Distribution: **CurseForge only**, same constraint as SF1 - the FTB utility
  stack is CF-only and Modrinth forbids inlining CF jars as overrides. Productive
  Frogs is CF-only too.

## Blockers (read before planning anything)

One blocker is open (2). Blocker 1 was resolved in fact and corrected in the SCRUB of 2026-11-08.

### 1. Productive Frogs 2.x is not published - RESOLVED (corrected 2026-11-08)

This was wrong. The CurseForge files page hides alpha files by default ("Show alpha files" is off), so the default view showed only the 1.21.1 releases and betas. With alphas shown, PF 2.0.0 alphas are published for 26.1.2 on NeoForge: alpha.2 (2026-07-09, file 8402058) and alpha.5 (2026-08-31, file 8774417), both type A. The newest is `v2.0.0-alpha.5`. There is no stable 2.0.0. Pinning with `packwiz cf add productive-frogs` needs alpha files allowed, and still needs to be tried. Verified by reading the CurseForge file pages on 2026-11-08.

### 2. Skyblock Builder has no 26.x build

Newest is 21.1.34 (1.21.1, 2026-08-06). This is the same mod that forced SF1's
rollback from 1.21.11 to 1.21.1, and it is the one dependency in the list with no
substitute.

The fallback is a datapack void world preset plus a structure-placed starter
island, which drops the dependency but also drops `/skyblock create` team
islands. **Undecided** - see the decision log's blockers section. Whichever way
it goes should be written up as D-4 before any worldgen work starts.

Lead, unvetted (2026-11-08): a different mod, "Sky Block Builder" (CurseForge slug `sky-block-mod`), lists `SkyBlockMod-26.1.2-1.0.0` for NeoForge 26.1.2 (2026-07-06) with a skyblock world preset, island templates and team management. It is not ChaoticTrials' Skyblock Builder, and its licence, dependencies and feature parity have not been checked.

## Current pin state

Six mods, all verified present for 26.1.2:

| Mod | Pin | Why |
|---|---|---|
| KubeJS | 8.0.4 | scripting spine; pulls Rhino |
| FTB Quests | 26.1.2.3 | quest book; pulls FTB Library + FTB Teams |
| Ex Deorum | 4.0 | the Builders' Sieve, which D-3 makes load-bearing (5.x is 26.2-only, do not take it) |

Productive Frogs is **not pinned yet**. It was held back for blocker 1, which is resolved (alpha.5 exists for 26.1.2); pinning it is the next step.

## Project conventions

Carried from SF1, and they earned their place there:

- **Docs filenames:** snake_case.
- **Line endings:** `.gitattributes` forces LF for source/config/docs and CRLF for
  `.bat`/`.cmd`/`.ps1`. Do not fight it.
- **After editing anything under `pack/`,** run `python tools/pack_refresh.py`
  (never bare `packwiz refresh`) and stage `pack/index.toml` + `pack/pack.toml` in
  the **same commit**. Nothing auto-catches a stale index, and FTB rewrites `.snbt`
  to CRLF on world load, which makes a bare refresh record hashes no committed
  file has.
- **Conventional Commits:** `feat:`, `fix:`, `refactor:`, `docs:`, `chore:`, `ci:`.
  The body explains the **why**.
- **ASCII punctuation only.** No em-dashes or en-dashes anywhere, including code
  comments and commit messages.
- **License:** MIT for pack-authored content; bundled mods keep their own.

## Scope discipline

This repo is a **content pack**. Java does not belong here - if a feature needs
Java, it goes in [productive-frogs](../productive-frogs) instead. SF1 proved the
other half of that rule too: when a *bundled third-party* mod mishandles our
items and its author is inactive, a gated mixin in Productive Frogs is a
legitimate, testable answer. See SF1's `docs/known_issues.md` Iron Furnaces
entries for the worked example.

Acceptable surfaces here: KubeJS scripts, datapack and resourcepack overrides,
mod configs, FTB Quests data, pack metadata, and docs.

## Not yet built

Honest inventory, so nobody assumes a thing exists:

- No CI, no release workflow, no `.githooks` content
- No quest chapters, no KubeJS scripts, no configs
- No `tools/` beyond `pack_refresh.py`; SF1's validator, generators and instance
  sync are **not** ported yet, and several are SF1-design-specific rather than
  portable
- No CurseForge project, no branding, no README worth the name
- No dev instance
