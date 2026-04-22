# Audio assets

Drop mp3 files here with these exact filenames. R1 (Shattered Vale in-realm) reuses `the_shattered_vale.mp3` — no separate file needed, so 19 unique files total.

## Main progression (13)

- `infernum_welcome.mp3` — **uploaded**
- `the_pull.mp3` — **uploaded** (sits inactive — track stays locked until scroll inventory + tutorial ship)
- `the_binding.mp3` — **uploaded**
- `shade.mp3` — **uploaded**
- `the_garrison.mp3` — pending
- `the_shattered_vale.mp3` — **uploaded**
- `sin_lords_anthem.mp3` — **uploaded**
- `the_codex.mp3` — **uploaded**
- `rift_walker.mp3` — **uploaded**
- `the_unnamed_one.mp3` — pending
- `sanctum_rising.mp3` — pending
- `the_rift_between.mp3` — **uploaded**
- `the_apex.mp3` — pending

## Realm tracks (6 — R1 reuses track 06's file)

- `vrathax_warfront.mp3` — **uploaded**
- `gilded_pit.mp3` — pending (unwritten)
- `the_stillness.mp3` — pending (unwritten)
- `mirror_maze.mp3` — pending (unwritten)
- `crumbling_throne.mp3` — pending (unwritten)
- `gorgethorn_maw.mp3` — pending (unwritten)
- `void_wastes.mp3` — pending (unwritten)

The game boots without any of these. Missing tracks stay silent when selected — the player element loads with an `error` event and playback stays paused. Deferred tracks don't unlock, so their missing files aren't visible to the player.
