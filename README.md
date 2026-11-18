# Macaw's Fences and Walls — a Horizon port

**Macaw's Fences and Walls** is a Minecraft mod. This repository is a **port of it to [Horizon](https://github.com/horizon-rust/horizon)**, the Rust engine for Minecraft Java 26.3. It carries the complete source of the port plus the content files it ships, and installs as a single `.hmod` package.

Upstream: [sketchmacaw/Fences](https://github.com/sketchmacaw/Fences) — licence **MIT**.

| | |
|---|---|
| Upstream mod | Macaw's Fences and Walls ([source](https://github.com/sketchmacaw/Fences)) |
| Ported to | Horizon 0b14f8a, Minecraft Java 26.3, mod API `0.2` |
| Package | `mcwfences.hmod` (install it with the Horizon launcher) |
| Licence | **MIT** — the upstream mod's licence; see [Licence and credit](#licence-and-credit) |

## What this port implements

- **The creative tab.** Upstream registers it in Java (`TabInit`), and a
- **The manifest** is port-owned (`horizon-mod.toml` with description and
- **Connectable states.** `minecraft:oak_fence` copies the same four boolean
- **Wall/fence post shapes.** The `*_wall` blocks are fence-class upstream, so
- **Gate `in_wall`.** `minecraft:oak_fence_gate` has `facing, in_wall, open,
- **All 4800 states have a model.** Gates' `variants` only name

## Not yet ported

- **Template numbers.** No NeoForge oracle here, so per-block hardness, blast
- **Wired fences do not hurt.** `WiredFence`/`StoneWiredFence.entityInside`
- **Metal fences and curved gates (30 blocks)** are not carried (see above):
- **Fuel.** Upstream's `FuelItemBlock`/`FuelItemBlockStackable` make the fence
- **Cheval-de-frise hitbox.** `check` reports 1 block with a shape of its own
- **Flammability is shared** (deviation 1): a stone or metal gate burns like a
- **Creative tab order** is by family then name, not upstream's registration
- **Advancements** (22 recipe unlocks) are carried as data and reference

## Installing

1. Install the [Horizon launcher](https://github.com/horizon-rust/horizon/releases) (0.2.70 or newer).
2. Add `mcwfences.hmod` to the instance's mods.
3. The package is pinned to a specific Horizon build; the launcher checks that pin.

## Licence and credit

Macaw's Fences and Walls was created by its upstream authors; the code, models and assets in the original mod
remain theirs and are used here under **MIT**. The Rust in this repository is a clean-room
rewrite for Horizon, not a translation of the original source.

- `LICENSE` — the upstream licence text.
- `LICENSE-NOTICE.md` — what this port carries and where it came from.
- The upstream project: https://github.com/sketchmacaw/Fences

## Technical details

```
horizon-mod.toml   package manifest (id, version, api, [native] pin)
Cargo.toml         the crate; depends on `horizon-mod-api` from the fetched SDK
src/               lib.rs (the one `impl Hooks`), runtime.rs (pure logic + tests), glue
assets/ data/      the content the package ships
tools/             content generators and the e2e scenario
```

- Build: `cargo horizon-mod build` (packages; it does not compile against the game).
- Test: `cargo test`, `cargo clippy --all-targets -- -D warnings`.
- In-game: `ports/tools/launcher-game.sh run mcwfences` in the campaign tree, or install the
  `.hmod` and play; the harness scenario is `tools/e2e.sh`.

This repository is generated from the campaign's port at `ports/mcwfences/`; the port's own
`notes.md` is the full record (decisions, traps, evidence).
