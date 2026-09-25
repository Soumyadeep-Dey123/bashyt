# bashyt

A lightweight YouTube search and player for the terminal.

`bashyt` combines **yt-dlp**, **fzf**, and **mpv** to let you search YouTube, interactively select a video, and play it directly from the terminal — without downloading the video.

## Features

- 🔎 Search YouTube directly from the terminal
- 🎯 Interactive result selection with `fzf`
- ▶️ Playback through `mpv`
- 🚫 No video downloads
- ⚡ Direct YouTube streaming through `yt-dlp`
- 🎥 VP9 video up to 1080p by default
- 🔊 Opus audio
- 🖥️ Works with mpv's hardware acceleration
- 🐚 Written entirely in Bash
- 🪶 Lightweight and dependency-friendly

## Requirements

- Bash
- [yt-dlp](https://github.com/yt-dlp/yt-dlp)
- [fzf](https://github.com/junegunn/fzf)
- [mpv](https://mpv.io/)

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/bashyt.git
cd bashyt
```

Make the script executable:

```bash
chmod +x bashyt
```

Install it into your local executable path:

```bash
mkdir -p ~/.local/bin
ln -s "$(pwd)/bashyt" ~/.local/bin/bashyt
```

Make sure `~/.local/bin` is in your `PATH`.

## Usage

### Search directly

```bash
bashyt "raj shamani neurologist"
```

This searches YouTube and presents the results through `fzf`.

Select a video and press **Enter** to play it with mpv.

### Interactive search

Run:

```bash
bashyt
```

You will be prompted for a search query:

```text
Search YouTube: raj shamani neurologist
```

## How it works

```text
Search query
     │
     ▼
   yt-dlp
     │
     ▼
YouTube search results
     │
     ▼
    fzf
     │
     ▼
Selected video
     │
     ▼
    mpv
     │
     ▼
Direct YouTube stream
```

`bashyt` does not download the selected video. `yt-dlp` is used to search YouTube and provide the selected video's URL to `mpv`.

## Playback

The default format selection is:

```text
bestvideo[vcodec^=vp9][height<=1080]+bestaudio/best
```

This prioritizes VP9 video up to 1080p with the best available audio, falling back to another suitable format when necessary.

## Why bashyt?

There are many YouTube terminal applications. `bashyt` aims to stay simple:

- no API keys
- no database
- no web interface
- no third-party search service
- no video downloads
- just Bash, yt-dlp, fzf and mpv

## Contributing

Issues, improvements and pull requests are welcome.

If you have an idea for a feature or find a bug, feel free to open an issue.

## License

This project is licensed under the MIT License.
