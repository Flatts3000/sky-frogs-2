# Changelog

Follows [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/) and [SemVer](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0] - 2026-11-08

First tagged build of Sky Frogs 2. This is a pre-alpha scaffold and it is not playable: there are no quests, no starter island and no pack scripts or configs yet. It exists to prove the dependency stack loads together on Minecraft 26.1.2 and to give the release pipeline something to ship.

### Added

- Repo scaffolding: a packwiz pack targeting Minecraft 26.1.2 on NeoForge 26.1.2.126 (Java 25).
- Productive Frogs 2.0.0-alpha.5, the pack's central dependency. It is alpha only; there is no stable 2.x yet.
- KubeJS 8.0.8, FTB Quests 26.1.2.10 and Ex Deorum 4.0, plus the Rhino, FTB Library 26.1.2.12 and FTB Teams 26.1.2.5 dependencies they pull. Ex Deorum stays on 4.0 on purpose, because 5.x is 26.2-only.
- The Sky Frogs 2 decision log (D-1 to D-3), the Sky Frogs 1 retrospective it draws on, and the held player-feedback capture.
- `tools/pack_refresh.py`, carried over from Sky Frogs 1.
- Community and repo files: contributing guide, code of conduct, security policy, notice, issue and PR templates, and a tag-driven release workflow that publishes to GitHub, CurseForge and Discord.

### Known issues

- Skyblock Builder has no 26.x build, so there is no skyblock world preset yet. The worldgen approach is undecided.
- The pack has not been launched in a game, so the NeoForge 26.1.2.126 and Productive Frogs alpha combination is untested.
