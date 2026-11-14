# bashyt

A lightweight YouTube search and player for the terminal.

`bashyt` combines **yt-dlp**, **fzf**, and **mpv** to let you search YouTube, interactively select a video, and play it directly from the terminal — without downloading the video.

## Features

- 🔎 Search YouTube directly from the terminal
- 🎯 Interactive result selection with `fzf`
- ▶️ Playback through `mpv`
- 🚫 No video downloads
- ⚡ Direct YouTube streaming through `yt-dlp`
- 🎥 Best available quality — capped by your screen resolution and connection speed
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
https://github.com/Soumyadeep-Dey123/bashyt.git
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

`bashyt` plays the best available quality by default, capped by two things:

- **Your screen** — the video never exceeds your screen height (detected with `xrandr`/`xdpyinfo`).
- **Your connection** — a short download probe (`curl`) before playback picks the highest resolution your bandwidth can sustain: 4K on fast connections, down to 480p on very slow ones.

If a cap can't be detected, the strongest known cap is used instead. To pin an exact format, set the `BASHYT_FORMAT` environment variable (e.g. `BASHYT_FORMAT='bestvideo[height<=720]+bestaudio/best' bashyt "query"`).

The mpv window autofits to 90% of your screen size, preserving the video's aspect ratio. Override it with the `BASHYT_AUTOFIT` environment variable (e.g. `BASHYT_AUTOFIT=75%x75% bashyt "query"`).

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

## Version history

- **1.2.0** — Best available quality by default, capped by your screen resolution and connection speed; `BASHYT_FORMAT` env var to pin an exact format.
- **1.1.0** — The mpv window now autofits to 90% of the screen; `BASHYT_AUTOFIT` env var to override.
- **1.0.1** — Initial release: YouTube search via yt-dlp, selection with fzf, playback with mpv.

## License

This project is licensed under the MIT License.
