# INFERNUM

Dark gothic gacha game. Single `index.html` with no build step.

## Music system

The music player expects the following audio files in `assets/audio/`:

| File | Unlock condition | Notes |
|---|---|---|
| `infernum_welcome.mp3` | Unlocked by default | Plays first on fresh saves; intended to score character creation once that screen exists |
| `rift_walker.mp3` | Unlocked by default | Plays second in default rotation |
| `sin_lords_anthem.mp3` | Bind a Sin Lord demon | |
| `the_binding.mp3` | Perform 10 total summons | |
| `the_unnamed_one.mp3` | Bind a Void Primordial demon | |
| `the_shattered_vale.mp3` | Conquer the Shattered Vale (all 13 stages) | |

The game runs without any audio files — missing tracks stay silent and skip on auto-advance.

## State

All state persists to `localStorage` under the key `inf_hub`:

- `S.musicUnlocked` — array of unlocked track IDs
- `S.musicPlaylist` — array of track IDs in active rotation
- `S.musicVolume` — number 0 to 1
- `S.musicEnabled` — boolean for master mute
- `S.realmProgress` — object mapping realm ID to conquered stage count

## Realm progression (dev note)

Until the battle system is built, clicking a realm on the Realms screen advances it by one stage. 13 clicks to fully conquer the Shattered Vale and unlock its track. Replace the body of `enterRealm()` when the real battle system is wired up — just keep the call to `Music.checkUnlocks()` after `save()`.

## Character creation (not yet built)

The welcome track is designed to play during character creation. Until that screen exists, the track simply plays first for any fresh save and then auto-advances to Rift Walker. When character creation is added, no music changes are needed — the track is already playing by the time any creation UI appears.

## Deploy

Static hosting. Works on Vercel by pointing at the repo root — no build step, no config needed.
