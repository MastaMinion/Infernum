# INFERNUM

Dark gothic gacha game. Single `index.html` with no build step.

## Music system

20 track entries wired into `TRACKS`. Some unlock against existing systems, some are deferred (check returns false) until the system they depend on ships. All 20 display in the full playlist screen — unlocked ones can be toggled on/off by the player, locked ones show their condition text.

Audio files live in `assets/audio/`. Filename must match the `id` in the TRACKS entry exactly (e.g. `the_pull.mp3` for `id:'the_pull'`).

### Main progression (13)

| # | File | Unlock condition | Status |
|---|---|---|---|
| 01 | `infernum_welcome.mp3` | Unlocked by default | Live |
| 02 | `the_pull.mp3` | Receive your first scroll | **Deferred** (needs scroll inventory + tutorial) |
| 03 | `the_binding.mp3` | Complete your first pull | Live |
| 04 | `shade.mp3` | Bind all 5 Shades | Live |
| 05 | `the_garrison.mp3` | Garrison your first demon | **Deferred** (needs garrison assignment UI) |
| 06 | `the_shattered_vale.mp3` | Conquer the Shattered Vale | Live |
| 07 | `sin_lords_anthem.mp3` | Bind your first Sin Lord | Live |
| 08 | `the_codex.mp3` | Bind 14 demons — half the roster | Live |
| 09 | `rift_walker.mp3` | Bind all three Archdemons — Bal'zeth, Xerathos, Malvekis | Live |
| 10 | `the_unnamed_one.mp3` | Pull your first Void Primordial | Live |
| 11 | `sanctum_rising.mp3` | Conquer all 8 realms | **Deferred** (needs realm unlocking) |
| 12 | `the_rift_between.mp3` | Bind all 28 demons | Live |
| 13 | `the_apex.mp3` | Complete everything — all realms, full codex | **Deferred** (needs realm unlocking + cinematic system) |

### Realm tracks (7)

Each plays while inside its realm. R1 (Shattered Vale) reuses track 06's file — no separate file needed.

| # | File | Unlock condition | Status |
|---|---|---|---|
| R2 | `vrathax_warfront.mp3` | Enter Vrath'ax Warfront | **Deferred** (needs realm unlocking) |
| R3 | `gilded_pit.mp3` | Enter Gilded Pit | **Deferred** |
| R4 | `the_stillness.mp3` | Enter The Stillness | **Deferred** |
| R5 | `mirror_maze.mp3` | Enter Mirror Maze | **Deferred** |
| R6 | `crumbling_throne.mp3` | Enter Crumbling Throne | **Deferred** |
| R7 | `gorgethorn_maw.mp3` | Enter Gorgethorn's Maw | **Deferred** |
| R8 | `void_wastes.mp3` | Enter The Void Wastes | **Deferred** |

### Deferred tracks

Each deferred track's entry in `TRACKS` has a `check:function(){return false;}` stub with a `TODO:` comment directly above it spelling out the exact condition code for when the dependency ships. When you're ready to wire one up, uncomment / paste the code in the TODO and change the check.

### How unlock notifications fire

`Music.checkUnlocks()` runs after each pull and after each realm stage conquest. Any track whose `check()` flips from false to true gets added to `S.musicUnlocked` and `S.musicPlaylist`, and a toast renders in the top-right.

### Screen-scoped playback

Not yet implemented. Current playback is "single rotation across all screens" — unlocked tracks that are toggled on cycle in sequence regardless of which screen the player is on. The spec calls for Codex tracks to play on Codex screen, Garrison tracks on Garrison, etc. That's a separate refactor for later.

## State

All state persists to `localStorage` under the key `inf_hub`:

- `S.musicUnlocked` — array of unlocked track IDs
- `S.musicPlaylist` — array of track IDs currently toggled on in the rotation
- `S.musicVolume` — number 0 to 1
- `S.musicEnabled` — boolean for master mute
- `S.realmProgress` — object mapping realm ID to conquered stage count

## Realm progression (dev note)

Until the battle system is built, clicking a realm on the Realms screen advances it by one stage. 13 clicks to fully conquer the Shattered Vale and unlock its track. Replace the body of `enterRealm()` when the real battle system is wired up — just keep the call to `Music.checkUnlocks()` after `save()`.

## Deploy

Static hosting. Works on Vercel by pointing at the repo root — no build step, no config needed.
