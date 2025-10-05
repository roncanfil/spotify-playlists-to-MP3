# 🎵 From Spotify Playlists to MP3

A Python script that downloads songs from YouTube and converts them to MP3 files with proper metadata, using Spotify playlist data exported as CSV files.

## 🚀 Features

- **Smart Playlist Processing**: Uses CSV files exported from Spotify playlists
- **YouTube Integration**: Automatically searches and downloads from YouTube
- **Rich Metadata**: Embeds artist, song, album, and YouTube URL into MP3 files
- **Duplicate Prevention**: Skips already downloaded songs for incremental updates
- **Dynamic Organization**: Creates folders named after your playlists
- **Clean Interface**: Beautiful progress indicators and loading animations
- **Command-Line Ready**: Simple command-line interface for easy automation

## 📋 Prerequisites

- Python 3.7 or higher
- Internet connection
- FFmpeg (for audio conversion)

## 🛠️ Installation

### 1. Check if Python is Installed

First, verify that Python is installed on your system:

**Check Python version:**
```bash
python --version
```

**Or try:**
```bash
python3 --version
```

You should see output like `Python 3.7.x` or higher. If you get a "command not found" error, you need to install Python first.

**Install Python:**
- **macOS**: Download from [python.org](https://www.python.org/downloads/) or use Homebrew: `brew install python`
- **Windows**: Download from [python.org](https://www.python.org/downloads/)
- **Linux**: Usually pre-installed, or use your package manager: `sudo apt install python3`

### 2. Install Python Dependencies

```bash
pip install pandas yt-dlp
```

### 3. Install FFmpeg

**macOS (using Homebrew):**
```bash
brew install ffmpeg
```

**Windows:**
- Download from [FFmpeg official website](https://ffmpeg.org/download.html)
- Add to your system PATH

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install ffmpeg
```

## 📊 Step 1: Export Your Spotify Playlist

1. Go to [Exportify](https://exportify.app/)
2. Log in with your Spotify account
3. Select the playlist you want to download
4. Click "Export" to download the CSV file
5. Save the CSV file to your desired location

> **Note**: Exportify is a third-party service that exports your Spotify playlists as CSV files. Make sure you trust the service before logging in.

## 🎯 Step 2: Download Your Music

### Basic Usage

```bash
python download.py your_playlist.csv
```

### Examples

```bash
# Download from a playlist called "Summer Hits"
python download.py summer_hits.csv

# Download from a playlist in another folder
python download.py /path/to/my_playlist.csv

# Download from multiple playlists
python download.py rock_classics.csv
python download.py jazz_favorites.csv
```

## 📁 Output Structure

The script creates organized folders based on your playlist names:

```
your_playlist/
├── Artist Name - Song Title.mp3
├── Another Artist - Another Song.mp3
└── ...
```

**Example:**
```
summer_hits/
├── The Chainsmokers - Something Just Like This.mp3
├── Coldplay - Viva La Vida.mp3
└── Ed Sheeran - Shape of You.mp3
```

## 🎵 MP3 Metadata

Each downloaded MP3 file includes:

- **Title**: Song name from Spotify
- **Artist**: Artist name from Spotify
- **Album**: Album name from Spotify
- **Comment**: Original YouTube URL

## 🔄 Incremental Downloads

One of the best features is **duplicate prevention**:

- ✅ **First run**: Downloads all songs from the playlist
- ✅ **Subsequent runs**: Only downloads new songs you've added
- ✅ **Smart skipping**: Shows which songs already exist

### Example Output

```
📁 Output directory: my_playlist
📊 Found 100 songs in playlist
==================================================
⏭️  Skipping (already exists): The Chainsmokers - Something Just Like This
🎵 Downloading: New Artist - New Song
   Album: New Album
🎵 Downloading: New Artist - New Song... ✅
==================================================
📈 Summary:
   Total songs: 100
   Downloaded: 2
   Skipped (already exist): 98
```

## 🎨 Progress Indicators

The script provides beautiful visual feedback:

- **📁** Shows output directory
- **📊** Displays total songs found
- **⏭️** Indicates skipped songs (already exist)
- **🎵** Shows downloading progress with animated dots
- **✅** Confirms successful downloads
- **❌** Reports any errors
- **📈** Final summary with statistics

## 🔧 Advanced Usage

### Custom CSV Column Names

If your CSV file uses different column names, modify these lines in the script:

```python
track_col = "Track Name"        # Change to your track column name
artist_col = "Artist Name(s)"   # Change to your artist column name
album_col = "Album Name"        # Change to your album column name
```

### Changing MP3 Quality

By default, the script downloads MP3s at 320 kbps (highest quality). To change the quality for smaller file sizes, modify line 67 in the `create_ydl_opts` function:

```python
'preferredquality': '320',  # Change this value
```

**Quality Options:**
- `'320'` - Highest quality (default, ~10-15 MB per song)
- `'256'` - High quality (~8-12 MB per song)
- `'192'` - Good quality (~6-9 MB per song)
- `'128'` - Standard quality (~4-6 MB per song)
- `'96'` - Lower quality (~3-4 MB per song)

**Example for smaller files:**
```python
'preferredquality': '192',  # Good quality with smaller file size
```

### Batch Processing

Create a simple batch script to process multiple playlists:

**Windows (batch_convert.bat):**
```batch
@echo off
python download.py playlist1.csv
python download.py playlist2.csv
python download.py playlist3.csv
pause
```

**macOS/Linux (batch_convert.sh):**
```bash
#!/bin/bash
python download.py playlist1.csv
python download.py playlist2.csv
python download.py playlist3.csv
```

## 🚨 Troubleshooting

### Common Issues

**"FFmpeg not found" error:**
- Make sure FFmpeg is installed and in your system PATH
- Test with: `ffmpeg -version`

**"CSV file not found" error:**
- Check the file path is correct
- Make sure the CSV file exists

**"No audio format found" error:**
- Some YouTube videos may not have audio
- The script will skip these and continue

**"Permission denied" error:**
- Make sure you have write permissions in the output directory
- Try running with administrator/sudo privileges if needed

### Getting Help

If you encounter issues:

1. Check that all dependencies are installed correctly
2. Verify your CSV file format matches the expected columns
3. Ensure you have a stable internet connection
4. Check that the YouTube videos are available and not region-locked

## 📝 CSV File Format

The script expects CSV files with these columns (from Exportify):

- `Track Name`: The name of the song
- `Artist Name(s)`: The artist(s) who performed the song
- `Album Name`: The album the song belongs to

## ⚖️ Legal Notice

This tool is for personal use only. Please respect:

- **Copyright laws** in your country
- **YouTube's Terms of Service**
- **Spotify's Terms of Service**
- **Artist and label rights**

Only download music you have the right to access or own.

## 🤝 Contributing

Feel free to submit issues, feature requests, or pull requests to improve this tool!

## 📄 License

This project is for educational purposes. Use at your own risk and ensure compliance with applicable laws and terms of service.

---

**Happy downloading! 🎵**

*Made with ❤️ for music lovers who want to enjoy their playlists offline.*
