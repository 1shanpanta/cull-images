# Cull

Open a folder of photos and send each one left or right. You decide what the two arrows do.

Each arrow is set independently to one of three things:

- **Delete** — removed from the folder
- **Keep** — left exactly where it is
- **Move to…** — moved into a folder you choose

So "keep or bin" is left = Delete, right = Keep. Pulling the good shots off a phone import is left = Keep, right = Move to. Splitting a shoot in two is Move to on both sides. Same motion every time, no modes to pick between.

Nothing is uploaded. No server, no analytics.

## Using it

1. **Open folder.**
2. **Change what the arrows do** if the defaults (delete / keep) are not what you want.
3. Send each photo: `←` / `→`, the two buttons, or drag the photo sideways. `Z` undoes. Click any thumbnail in the strip to jump back to it.
4. Press the button at the end. It says exactly what it will do, for example `Delete 12 and Move 30`.

Nothing on disk changes until that final button. Decisions are remembered per folder in `localStorage`, so closing the tab mid-pass is safe.

## How a move works

Read the file, write it to the destination, re-read what landed and compare byte length, and only then remove the original. If the sizes do not match, the original stays and the file is reported as left alone. Name clashes at the destination get a `-1`, `-2` suffix instead of overwriting. Choosing the source folder as a destination is refused.

## Browser support

Changing files needs the File System Access API: **Chrome or Edge, over https or localhost**. Elsewhere (Safari, Firefox, or a raw `file://` open) the folder still opens through `<input webkitdirectory>` and you can sort every photo, but Delete and Move are disabled and you leave with a copyable list instead.

## Phones

The folder picker only sees real filesystem paths. An iPhone never mounts as a drive on macOS, Android goes through Android File Transfer rather than a mounted volume, and mobile Chrome has no File System Access API. So: import the photos onto the computer first (Image Capture, AirDrop, SD card), then sort from there. Google Drive works if Drive for Desktop is installed, since it is an ordinary folder at that point.

## Run locally

```
python3 -m http.server 8811 --directory .
```

Open `http://localhost:8811`. Localhost is a secure context, so deleting and moving are enabled.

## Tech

One self-contained `index.html`: vanilla JS, no build step, no dependencies. Google Fonts (IBM Plex Sans + Mono) is the only external request.
