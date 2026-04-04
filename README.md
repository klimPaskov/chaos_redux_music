# Chaos Redux Music

Companion music mod for `Chaos Redux`.

This repository intentionally excludes audio files. The HOI4 script and mod
structure live here, while copyrighted source/output audio stays local and is
dropped into `music/` outside git.

## Purpose

`Chaos Redux Music` is a separate companion mod that depends on `Chaos Redux`.
It exists so music with separate copyright constraints can live outside the main
gameplay mod while still integrating with the same music IDs and systems.

## Repository policy

- Do not commit any sound files.
- Do not commit virtual environments or generated local tooling.
- Commit only the mod descriptor, music definitions, localisation, thumbnails,
  and documentation.

## Local setup

Place local audio files in `music/` with the filenames expected by the asset
definitions. If you add more tracks later:

1. Add or update the song definition in `music/chaos_redux_music_overrides.asset`
   or another `.asset` file.
2. If the song should appear in the station UI, add it to
   `music/chaosx_super_event_music.txt`.
3. If the goal is to replace an existing Chaos Redux super event track, do not
   add a new station entry. Reuse the exact existing song ID in a `.asset`
   definition instead so the base mod entry stays in place but its audio is
   swapped out by this mod.
4. Add matching localisation keys in
   `localisation/english/chaos_redux_music_l_english.yml`.
   Do not redefine vanilla localisation keys such as `maintheme`, or the game
   will log duplicate localisation warnings.
5. Do not redefine vanilla music IDs such as `maintheme` in a `.asset` file.
   Override the actual audio by replacing the vanilla filename instead.

## Integration strategy for future super event music

Chaos Redux super event music is currently keyed through song IDs defined in
`music/chaosx_super_event_music.asset` in the main mod. To replace one of those
tracks in the companion mod, define the exact same `name` in a music asset inside
this mod.

Using the same ID is the seamless part: the scripted GUI and event systems in the
main mod keep calling the same song, and the companion mod swaps only the audio
definition behind it. That is how the base tracks get effectively disabled and
replaced when this music mod is enabled: the original station slot and call site
stay the same, but the reused ID now points at the companion mod's audio file.

This mod also overrides the base mod's `music/chaosx_super_event_music.txt`
station file so the music player does not list internal
`chaosx_super_event_*` helper IDs. Only the curated visible entries should stay
in the station UI.

For the frontend loading theme, the mod does not redefine `maintheme`. Instead,
it supplies `music/hoi4mainthemeallies.ogg`, which replaces the vanilla file
used by the existing `maintheme` definition.
