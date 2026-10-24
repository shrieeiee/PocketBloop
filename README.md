# Pocket Bloop for Android

The cute pocket synth, rebuilt as a phone app. 17 styles, a 16-step sequencer for drums, melody (with chords) and bass, jam pads, dice randomisers and the singing blob mascot — all offline.

## Get the APK

**Easiest: let GitHub build it**

1. Create a new GitHub repo and push this folder to it.
2. Open the repo's **Actions** tab. The *Build APK* workflow runs on every push (or press *Run workflow*).
3. When it finishes (about 3–4 minutes), download the **pocket-bloop-apk** artifact, unzip it and copy `app-release.apk` to your phone.
4. Open it on the phone and allow "Install unknown apps" for your file manager when asked.

**Or with Android Studio:** open this folder, let it sync, then *Build → Build App Bundle(s) / APK(s) → Build APK(s)*.

The release APK is signed with the standard debug key so it installs straight away. Use your own keystore before publishing it anywhere.

## Touch controls

- **Tap** a step to toggle it. **Drag** across steps to paint (or erase) a whole run.
- On phones the grid shows **8 steps at a time** so each cell stays thumb-sized. Use **1–8 / 9–16** to switch; while playing it follows the playhead (turn that off in Knobs).
- **Tap a drum name** to mute it. Tap a note name to hear it.
- **Tap the blob** to make it sing. **Tap the style name** to open the style picker.
- **Jam** tab: multi-touch pads — slide a finger across them for a glissando.
- **Hold − / +** on the tempo to change it quickly.
- Every dice button, style change and Clear can be **undone** from the pop-up for a few seconds.
- Back button closes the style picker, then returns to the Beat tab, then exits.

## Built for low-end phones

- **Lite mode** switches on automatically on phones with about 2–3 GB of RAM (you can toggle it in Knobs). It swaps the convolution reverb for two cheap delay lines, thins supersaw/pad/reese voices, skips per-note vibrato, caps polyphony at 6 voices and uses a larger audio buffer, so playback stays glitch-free.
- The scheduler looks further ahead and skips forward after a hiccup instead of bursting late notes.
- The playhead is one element moved per step, the animation loop only runs while playing, and particles are capped.
- No `color-mix` or other very new CSS, so older WebViews render it correctly.
- No libraries at all: the APK is a tiny Java shell around one offline page (fonts bundled, ~200 KB of web assets).
- Playback stops when you leave the app; the screen stays awake only while it is playing.
- Your pattern, style and settings are remembered between launches.

## Fits any screen

- Portrait phones from 320 px wide up; short phones drop the style strip and use the tap-to-open picker instead so the grid keeps its space.
- Landscape and tablets switch to a two-column layout (mascot left, editor right) and show all 16 steps when there's room.
- Safe areas, notches and gesture bars are padded by the app; light and dark mode follow the system.

Needs Android 7.0 or newer with an up-to-date Android System WebView (updated through the Play Store).

## Layout

```
app/src/main/assets/www/index.html   the whole app (synth + UI)
app/src/main/assets/www/fonts/       bundled fonts (SIL Open Font License)
app/src/main/java/.../MainActivity.java   WebView shell, insets, haptics, keep-screen-on
.github/workflows/build-apk.yml      builds the APK on GitHub
```
