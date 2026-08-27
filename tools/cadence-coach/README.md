# Cadence Coach

A single-page speech-pace meter for interviews. Open it, park it beside your
call, and it tells you when you're outrunning the room.

## Running it

It's one self-contained HTML file with no build step and no dependencies.

- **Locally:** open `index.html` in Chrome, Edge, Firefox or Safari.
- **On a phone:** it needs HTTPS, so serve it (`npx serve tools/cadence-coach`)
  or use the published Artifact link.

Grant microphone access when asked. Wear headphones — otherwise the mic hears
your interviewer too and the numbers drift.

## How it measures pace

There is no speech recognition involved. Audio never leaves the page, and
nothing is recorded, stored, or transcribed.

1. Mic → `ScriptProcessorNode` → RMS loudness per 256-sample hop (~5 ms).
2. An envelope follower (fast attack, slower release) and an adaptive noise
   floor split the signal into voiced and silent hops.
3. Syllable nuclei are counted as envelope peaks followed by a ≥3.5 dB dip,
   with a 90 ms refractory gap — the amplitude-envelope method used in
   phonetics for automatic syllable counting.
4. Words per minute = syllables ÷ 1.4 syllables-per-word, over a rolling
   6-second wall-clock window. Because the window includes silence, pausing
   lowers the number, which is what a listener actually experiences.

Against synthetic speech-like signals the counter lands within ~1% of ground
truth from 3 to 7 syllables/second, and the resulting WPM within ~3%.

**Calibration** removes the remaining per-voice, per-mic error: you read a
passage of exactly 53 syllables and 44 words, and the app stores
`53 / peaks_detected` as a correction factor. It also measures your natural
reading pace and picks a target band from it.

## What it reacts to

| Signal | Meaning |
|---|---|
| Pace above the target band for 3 s | "ease off" — finish the sentence, then pause |
| 26 s with no pause ≥ 300 ms | "take a breath" |

Nudges are visual, plus `navigator.vibrate` where the device supports it
(Android; iOS Safari ignores it). Cues are rate-limited to one per 14 s.

A silent gain node keeps the AudioContext live so the browser doesn't throttle
analysis while the window sits behind your video call.

## Settings and storage

Target preset, calibration factor, and the last 8 session summaries are kept in
`localStorage`, wrapped so the page still works when storage is unavailable.
