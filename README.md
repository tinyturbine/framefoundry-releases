# FrameFoundry releases

Each release here carries one version of FrameFoundry for Windows:

- `FrameFoundry-v<version>-win64.zip` - the portable app. Unzip it anywhere you can write to and run `FrameFoundry.exe`. The first run gets the app's own Python, ffmpeg and the engines this PC can run (the This PC page), into that same folder.
- `FrameFoundry-v<version>-win64.zip.sha256` - the zip's SHA-256.

A copy that is already installed checks here when it starts. When a newer version is out, the gear in the title bar turns amber; Settings' version then downloads it, checks it against its SHA-256, and switches over when the app restarts. Your projects, models and tools stay as they are.

This repository holds releases only.