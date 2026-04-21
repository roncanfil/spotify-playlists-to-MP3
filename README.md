# 🎵 From Spotify Playlists to MP3 / FLAC

A Python script that downloads songs from YouTube using Spotify playlist data exported as CSV files. It writes **MP3** (default) or **FLAC** with embedded metadata and skips tracks you already have.

## 🚀 Features

- **Smart playlist processing**: CSV files exported from Spotify (e.g. via Exportify)
- **YouTube integration**: Searches with `ytsearch1` and downloads the best match
- **Formats**: **MP3 @ 192 kbps** by default, or **FLAC** (best available audio stream) via an optional argument
- **Rich metadata**: Title, artist, album, and original YouTube URL (via FFmpeg)
- **Duplicate prevention**: Skips files that already exist for the chosen format
- **Folder layout**: Output folder named after the CSV filename (without extension)
- **CLI**: `python download.py playlist.csv` or `python download.py playlist.csv flac`

## 📋 Prerequisites

- Python 3.8+ recommended (3.7 may work; use a current Python for best compatibility)
- Internet connection
- FFmpeg (for conversion and metadata)
- A recent **yt-dlp** (YouTube changes often; upgrade if downloads fail with HTTP 403)

## 🛠️ Installation

### 1. Python

```bash
python3 --version
```

Install if needed: [python.org](https://www.python.org/downloads/) or `brew install python` on macOS.

### 2. Dependencies

Using a virtual environment is recommended:

```bash
python3 -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -U pip
pip install pandas "yt-dlp[default]"
```

`yt-dlp[default]` pulls in optional pieces (e.g. EJS helpers) that YouTube extraction often needs.

### 3. FFmpeg

**macOS (Homebrew):**

```bash
brew install ffmpeg
```

**Windows:** [FFmpeg downloads](https://ffmpeg.org/download.html) — add `ffmpeg` to your PATH.

**Linux (Debian/Ubuntu):**

```bash
sudo apt update && sudo apt install ffmpeg
```

## 📊 Step 1: Export your Spotify playlist

1. Open [Exportify](https://exportify.app/)
2. Log in with Spotify
3. Choose a playlist and export CSV
4. Save the file where you will run the script

> Exportify is a third-party site; only use it if you are comfortable signing in there.

## 🎯 Step 2: Download your music

### MP3 (default, 192 kbps)

```bash
python download.py your_playlist.csv
```

### FLAC (best audio stream YouTube offers, written as `.flac`)

```bash
python download.py your_playlist.csv flac
```

`flac` must be the **second** argument exactly (see `python download.py -h`).

### Examples

```bash
python download.py summer_hits.csv
python download.py /path/to/my_playlist.csv
python download.py rock_classics.csv flac
```

On startup the script prints the output folder and format, for example:

- `Format: MP3 @ 192 kbps`
- `Format: FLAC (bestaudio → flac, lossless container)`

YouTube streams are usually lossy; FLAC mode avoids an extra **lossy** encode (MP3) and stores the decoded audio in a lossless container. It does not invent detail beyond the source stream.

## 📁 Output structure

The script creates a folder named after the CSV (filename without `.csv`):

**MP3:**

```text
your_playlist/
├── Artist Name - Song Title.mp3
└── ...
```

**FLAC:**

```text
your_playlist/
├── Artist Name - Song Title.flac
└── ...
```

Skip logic is per extension: a track skipped as existing `.mp3` is not skipped automatically when you re-run in FLAC mode (and vice versa).

## 🎵 Metadata

Embedded fields (MP3 and FLAC):

- **Title** — track from CSV  
- **Artist** — artist from CSV  
- **Album** — album from CSV  
- **Comment** — original YouTube URL (when resolved)

## 🔄 Incremental downloads

- First run: downloads all missing tracks  
- Later runs: only new rows / missing files  
- Skipped tracks are listed with ⏭️  

## 🎨 Progress output

The script prints folder, counts, album lines, per-song download lines with a spinner, ✅ / ❌ per track, and a short summary at the end.

## 🔧 Advanced usage

### CSV column names

If your export uses different headers, edit these in `download.py`:

```python
track_col = "Track Name"
artist_col = "Artist Name(s)"
album_col = "Album Name"
```

### Changing MP3 bitrate

Default is **192** kbps in `create_ydl_opts` (MP3 branch), key `preferredquality`. Typical values: `'128'`, `'192'`, `'256'`, `'320'`.

### Batch processing

**macOS / Linux:**

```bash
#!/bin/bash
python download.py playlist1.csv
python download.py playlist2.csv flac
```

**Windows:** same commands in a `.bat` file.

## 🚨 Troubleshooting

| Issue | What to try |
|--------|-------------|
| FFmpeg not found | `ffmpeg -version`; fix PATH or install FFmpeg |
| CSV not found | Check path; quote paths with spaces |
| `HTTP Error 403` / download fails | `pip install -U "yt-dlp[default]"` |
| No audio / odd failures | Video may be blocked or audio-less; try another upload |

## 📝 CSV format (Exportify)

Expected columns:

- `Track Name`
- `Artist Name(s)`
- `Album Name`

## ⚖️ Legal notice

For **personal use** only. Respect copyright, YouTube’s and Spotify’s terms, and rights holders. Only download what you are allowed to use.

## 🤝 Contributing

Issues and pull requests welcome.

## 📄 License

Educational / personal tooling. Use at your own risk and comply with applicable law and terms of service.

---

**Happy downloading.**
