# FrameFoundry

**Take media apart, build something new.**

FrameFoundry is a Windows desktop app for restoring and re-editing TV shows
and films from DVD rips, downloads and other sources. Bring in a season,
clean it up shot by shot - lift burned-in titles and watermarks, repair fades
and dissolves, upscale - then cut your own edit and deliver a finished file.

It is built for SD footage first (480-line DVD sources), and handles 4K too.

> **Status:** pre-alpha, v0.3.x. It works, it is rough in places, and it
> changes often.

This repository holds the releases. Download the latest from
[Releases](../../releases/latest).

---

## What it does

### Bring footage in
- **Projects and collections** - a project holds a series, a film, or a mix.
  Add videos from files, links, or a disc (via MakeMKV).
- **Knows the show** - links a collection to its show and episode guide, files
  each video to its episode, and keeps aired order or DVD order.
- **Several versions of one episode** - pair a DVD rip with a download, line
  them up frame for frame, compare them side by side in A|B, take colour from
  one, or replace footage from the other.

### Measure it
- **Scans** find the cuts, how the picture moves, its colour, its sound and
  its subtitle tracks. The cheap scans run at import; the heavier ones run on
  request, in the background.
- **On-screen text found for you** - title cards, credits and watermarks are
  located and read (OCR), so they can be checked and removed.
- **Interlacing, 3:2 film cadence and pixel shape** are detected, and
  **Prep** makes one clean, progressive base file that every later step
  works from, encoded on the GPU where it can be. Dot crawl and rainbowing
  are found and mended in prep.

### Shots and cuts
- The video is laid out as a strip of shots. Check the cuts, add, move or
  take them out, group shots into sets, and mark stretches.
- Long shots, fades, dissolves and black runs are flagged on the strip.

### Repair
- **Edge trim** for dirty frame edges.
- **Fades, dissolves and wipes** repaired - the other shot un-mixed from each
  side, so each shot stands on its own.
- **Black runs** found and tidied.

### Remove
- **Text and watermark removal** with a mask fitted to the lettering
  (letter shapes fitted through the detected font, type-on reveals tracked),
  then filled by video inpainting (ProPainter) or by a clean transfer from
  another copy of the same footage.
- **Mosquito noise** around removed text cleaned up.
- **The review room** to judge every fill, a **mask room** to correct one by
  hand, and a **paint room** for anything else you want painted out.
- **Removal touches only the fill** - every pixel outside the mask stays
  bit-exact.

### Enhance
- **Upscaling** with SeedVR2, to a target size, with clean-up dials before
  and after.
- **Smooth motion** frame interpolation (RIFE).
- **Film grain** put back after the upscale, matched per clip, with a live
  preview.
- **Assemble enhanced** rebuilds the full video from the enhanced shots.

### Stock footage and credits
- **Stock footage** - the same shot reused across episodes is found by sound
  and set exactly by picture. Pick the best copy, remove its text once, and
  the winner rides every use.
- **Credits** - opening and end credits are found and the names read into a
  list you can check, kept even after the credits are removed from the
  picture. Combined credits for an edit.

### Sound and lines
- Every audio track, a **stereo downmix**, and **stems** (dialogue, music,
  effects) split from any channel layout.
- **Transcripts** per audio track (Whisper), the file's own subtitles read at
  import, and the words editable on their own lane.
- Audio scans for sound health and content tagging.

### Edit and deliver
- **Edits** - lay clips from any of the project's videos end to end: a run of
  episodes, a recut of one, or a compilation. Gaps, seams with sound
  crossfades, chapters, extra audio and subtitle tracks.
- A **to-do list** and a **Ready?** check before delivery. Work done on a
  video carries into every edit that uses it.
- **Deliver** writes the finished file - a video or a whole edit, with its
  container, codecs and tracks chosen.

### Around the app
- **Undo and redo**, and every iteration of a video kept, so any step can be
  taken back.
- **This PC** checks the machine and downloads only what it can run - models
  and tools are fetched and SHA-checked, not assumed.
- **GPU first**, with a CPU fallback.
- **Self-updating**, with a one-press problem report (the log and the build
  stamp, nothing from your footage).

---

## Requirements

- Windows 11, 64-bit (the only system it has been tested on)
- An NVIDIA GPU for the heavy engines (inpainting, upscaling, interpolation).
  Without one, the app fetches only what the machine can run.
- MakeMKV, if you want to bring in discs

## Downloading

Each release here carries one version of FrameFoundry for Windows:

- `FrameFoundry-v<version>-win64.zip` - the portable app. Unzip it anywhere you can write to and run `FrameFoundry.exe`. The first run gets the app's own Python, ffmpeg and the engines this PC can run (the This PC page), into that same folder.
- `FrameFoundry-v<version>-win64.zip.sha256` - the zip's SHA-256.

Settings and logs live in `%LOCALAPPDATA%\FrameFoundry\`.

## Updating

A copy that is already installed checks here when it starts. When a newer version is out, the gear in the title bar turns amber; Settings' version then downloads it, checks it against its SHA-256, and switches over when the app restarts. Your projects, models and tools stay as they are.

## Built with

PySide6 (Qt) · FFmpeg · yt-dlp · VapourSynth · ProPainter · SeedVR2 · RIFE ·
FBCNN · EasyOCR · Whisper · Bandit · SepFormer · ECAPA · PANNs

Each of these keeps its own licence. ProPainter's terms are non-commercial.

---

© Tiny Turbine
