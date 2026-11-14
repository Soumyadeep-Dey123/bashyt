# AGENTS.md

Single-script project: the entire program is the executable Bash script `./bashyt` at the repo root. There is no build system, package manager, or test suite.

## Verification

- CI runs [ShellCheck](.github/workflows/shellcheck.yml) on every file in the repo (`scandir: .`) on every push/PR. Run locally before committing:
  ```bash
  shellcheck bashyt
  ```
- Manual test is just running it — `./bashyt "some query"` requires `yt-dlp`, `fzf`, and `mpv` in PATH (the script exits early with an error if any is missing). Opening an mpv playback window is expected, not a failure.

## Script gotchas

- `set -euo pipefail` is in effect; unbound variables and failed pipes abort the script.
- The `yt-dlp --print` format string uses **literal tab characters** as field separators. `fzf --delimiter`, `--with-nth`, and `cut -f1` all depend on them — preserve tabs exactly when editing that line.
- `BASHYT_CLIENTS` env var overrides the yt-dlp `player_client` extractor args (default: `tv,tv_simply,web_safari,android_vr`, chosen because these clients don't require a PO token). `BASHYT_AUTOFIT` similarly overrides the mpv window size (default: `90%x90%` of the screen). `BASHYT_FORMAT` pins an exact yt-dlp format string and bypasses all quality detection.
- The yt-dlp format is chosen **after** fzf selection, right before `exec mpv`, via `choose_format`: best available quality capped by min(screen height, connection tier). Screen height comes from `xrandr`/`xdpyinfo` (fails silently on bare Wayland without Xwayland); connection tier comes from a curl probe of `speed.cloudflare.com` — curl is optional, and a failed/missing probe degrades to the screen cap only. Tier mapping lives in `speed_height_cap`: ≥24 Mbps→4320, ≥10→2160, ≥6→1440, ≥3→1080, ≥1.5→720, else 480.

## Keep in sync

- `VERSION` is defined in the script; `--help` text and `README.md` duplicate it.
- `README.md` "Playback" section documents the quality behavior (screen/connection caps, `BASHYT_FORMAT` override). Keep it in sync when changing `DEFAULT_FORMAT`, `speed_height_cap`, or `choose_format`.
