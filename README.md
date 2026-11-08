# Sky Frogs 2

The Minecraft 26.x sequel to [Sky Frogs](https://www.curseforge.com/minecraft/modpacks/sky-frogs), built around [Productive Frogs](https://www.curseforge.com/minecraft/mc-mods/productive-frogs) 2.x.

**Status: scaffolding. Not playable, not released, no CurseForge project.**

## What is decided

Design lives in [`docs/decisions.md`](./docs/decisions.md), a live log of settled decisions. Three so far:

- **Slime Milk never runs dry.** Depletion is off and the catalysts that existed to manage it are gone. In Sky Frogs 1 the whole count line existed to service a burden the player should not have had, and the moment you unlocked the Endless catalyst the mechanic was over - roughly two thirds of the pack was played with it already invalidated.
- **No dark room.** Cave Slimes are not added to natural spawning at all. Vanilla hostile spawning was the single biggest failure point in Sky Frogs 1: 34 distinct people reported spawn trouble and every one of its failure conditions is invisible to the player.
- **Slime balls come off the sieve instead.** One line on the Builders' Sieve's dirt lane, and the existing bootstrap recipe does the rest. Nothing in the opening reads light level, player distance, mob cap or difficulty.

The evidence behind those calls is in [`docs/sf1_retrospective.md`](./docs/sf1_retrospective.md), distilled from 3,216 community messages across Sky Frogs 1's first two months.

## Blockers

One open, verified against live CurseForge data (2026-11-08):

1. ~~Productive Frogs 2.x is not published.~~ Resolved: PF 2.0.0 alphas are on CurseForge for 26.1.2 (latest `2.0.0-alpha.5`). The files page hides alphas by default, which is why this was missed. No stable 2.0.0 yet.
2. **Skyblock Builder has no 26.x build.** The one dependency with no substitute. The fallback is a datapack void world plus a structure-placed island, which costs team islands. Undecided.

## Building

Requires [packwiz](https://packwiz.infra.link/).

```sh
cd pack
packwiz refresh          # or, from the repo root: python tools/pack_refresh.py
```

Minecraft 26.1.2, NeoForge 26.1.2.126, Java 25.

## License

MIT for pack-authored content. Bundled mods retain their own licenses.
