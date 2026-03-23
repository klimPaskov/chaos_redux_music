# Chaos Redux Music

Companion music mod for `Chaos Redux`.

This repository intentionally excludes audio files. The HOI4 script and mod
structure live here, while copyrighted source/output audio stays local and is
dropped into `music/` outside git.

## Purpose

`Chaos Redux Music` is a separate companion mod that depends on `Chaos Redux`.
It exists so music with separate copyright constraints can live outside the main
gameplay mod while still integrating with the same music IDs and systems.

## Current implementation

The companion mod currently ships one frontend theme override:

- Song ID: `maintheme`
- File: `music/tomorrows_girls.ogg`
- Asset definition: `music/chaos_redux_music_overrides.asset`
- Localisation key: `maintheme`

The asset file redefines the existing `maintheme` song ID instead of inventing a
new one. This mirrors vanilla's `music/music.asset` and lets the companion mod
replace the loading/front-end theme that the game already knows how to play.

The same audio is also exposed as a normal song ID, `tomorrows_girls`, so it can
be assigned to the default soundtrack station without creating a separate station.

`music/chaos_redux_music_base_music.txt` is intentionally bound to `base_music`.
Future companion songs should be added there so they appear in the vanilla/main
music station rather than a custom Chaos Redux Music station.

## Repository policy

- Do not commit any sound files.
- Do not commit virtual environments or generated local tooling.
- Commit only the mod descriptor, music definitions, localisation, thumbnails,
  and documentation.

## Local setup

Place local audio files in `music/` with the filenames expected by the asset
definitions. For the current beta wiring:

- `music/tomorrows_girls.ogg` is the frontend loading theme via `maintheme`.
- `music/tomorrows_girls.ogg` is also exposed as `tomorrows_girls` in the
  default `base_music` station.

If you add more tracks later:

1. Add or update the song definition in `music/chaos_redux_music_overrides.asset`
   or another `.asset` file.
2. Add the song to `music/chaos_redux_music_base_music.txt` so it appears in
   the default music station.
3. Add matching localisation keys in
   `localisation/english/chaos_redux_music_l_english.yml`.

## Integration strategy for future super event music

Chaos Redux super event music is currently keyed through song IDs defined in
`music/chaosx_super_event_music.asset` in the main mod. To replace one of those
tracks in the companion mod, define the exact same `name` in a music asset inside
this mod.

Examples of existing IDs in the main mod:

- `default`
- `zombies_music`
- `world_revolution`
- `chaosx_super_event_1_0_5`
- `chaosx_super_event_1_1_0`
- `chaosx_super_event_1_1_5`
- `chaosx_super_event_1_2_0`
- `chaosx_super_event_1_2_5`
- `chaosx_super_event_1_3_0`
- `chaosx_super_event_2_0_5`
- `chaosx_super_event_2_1_0`
- `chaosx_super_event_2_1_5`
- `chaosx_super_event_2_2_0`
- `chaosx_super_event_2_2_5`
- `chaosx_super_event_2_3_0`
- `chaosx_super_event_3_0_5`
- `chaosx_super_event_3_1_0`
- `chaosx_super_event_3_1_5`
- `chaosx_super_event_3_2_0`
- `chaosx_super_event_3_2_5`
- `chaosx_super_event_3_3_0`
- `chaosx_super_event_4_0_5`
- `chaosx_super_event_4_1_0`
- `chaosx_super_event_4_1_5`
- `chaosx_super_event_4_2_0`
- `chaosx_super_event_4_2_5`
- `chaosx_super_event_4_3_0`
- `chaosx_super_event_5_0_5`
- `chaosx_super_event_5_1_0`
- `chaosx_super_event_5_1_5`
- `chaosx_super_event_5_2_0`
- `chaosx_super_event_5_2_5`
- `chaosx_super_event_5_3_0`

Using the same ID is the seamless part: the scripted GUI and event systems in the
main mod keep calling the same song, and the companion mod swaps only the audio
definition behind it.
