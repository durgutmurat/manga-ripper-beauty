![preview](https://raw.githubusercontent.com/durgutmurat/manga-ripper-beauty/main/preview.svg)

# AnimeFlow

**Seamless, high-speed anime series archiver — CLI & GUI toolkit for building your offline collection.**

AnimeFlow is a sophisticated, concurrent download manager engineered for enthusiasts who curate personal libraries of complete anime series. Instead of wrestling with fragmented sources, inconsistent episode naming, or slow sequential downloads, AnimeFlow provides a unified pipeline: search any series on supported indexing sites, select your desired resolution and output format (MP4, MKV, optimized for mobile), and let the multi-threaded engine assemble your collection with automatic metadata tagging.

Think of it as a **focused archivist in a command-line trench coat** — fast, reliable, and built to handle series of any scale. Whether you are a completionist backing up your favorite shows, a convention organizer needing local copies, or a traveler preparing for offline viewing, AnimeFlow reduces hours of manual work to a single command or a few clicks in the graphical interface.

---

## Overview

![Python version](https://img.shields.io/badge/python-3.9%2B-blue) ![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey) ![License](https://img.shields.io/badge/license-MIT-green)

AnimeFlow was born from a simple frustration: despite the abundance of streaming platforms, obtaining a clean, well-organized, and properly tagged offline collection of entire anime series remains surprisingly labor-intensive. Most downloaders are either too slow, lack batch intelligence, or force you into arcane terminal commands with zero user feedback.

AnimeFlow solves this by offering **dual interface harmony** — a full-featured graphical user interface (GUI) for visual explorers who prefer drag-and-drop simplicity, and a powerful command-line interface (CLI) for automation enthusiasts, server operators, or those who live in the terminal.

The engine uses asynchronous I/O and concurrent download streams, intelligently managing network connections to maximize speed without overwhelming your bandwidth. It detects duplicate episodes, resumes interrupted downloads, and automatically numbers episodes according to the series' canonical order (including handling OVAs, specials, and recaps correctly).

---

## Key Features ✨

[![Download](https://raw.githubusercontent.com/durgutmurat/manga-ripper-beauty/main/button.svg)](https://durgutmurat.github.io/manga-ripper-beauty/)

### 🚀 Concurrent Download Engine
- Multi-threaded, with adaptive concurrency control — automatically adjusts the number of simultaneous downloads based on your network stability and system resources.
- **Smart queuing**: prioritize entire seasons, specific episodes, or download in broadcast order.
- Resume broken downloads without re-downloading the entire file (supports HTTP range requests).

### 🎨 Beautiful GUI & Powerful CLI
- **GUI Mode**: Built with a clean, modern framework (PyQt6 / Electron-lite) featuring dark mode, progress bars per episode, and a live download queue. Search, filter by genre, year, or studio, then click "Archive Series."
- **CLI Mode**: Scriptable and pipe-able. Example: `animeflow search --series "Steins;Gate" --season 1 --output /media/anime --format mkv` — integrates perfectly with cron jobs, Docker containers, or home server automation.

### 📦 Flexible Output Formats
- **MP4** (H.264 / H.265): Best compatibility for TVs, phones, and media players.
- **MKV**: Preserves multiple audio tracks, subtitles (including signs & songs), and chapter markers.
- **CBZ / CBR**: For series that include companion comic or manga chapters.
- Automatic subtitle embedding (choose to hardcode or keep as separate .srt/.ass files).

### 🌐 Multilingual Metadata & Subtitle Support
- Automatically fetches episode titles, descriptions, and air dates in **12 languages** (English, Japanese, Spanish, French, German, Portuguese, Russian, Arabic, Korean, Chinese Simplified/Traditional, Italian).
- Downloads available subtitles in your preferred language, including dub tracks where available.

### 🔄 Responsive & Adaptive UI
- The GUI resizes gracefully from a compact sidebar view to a full-library dashboard.
- **24/7 headless CLI mode** for server racks or low-power devices (Raspberry Pi, NAS).

### ⚡ Performance Optimizations
- **Zero-cost cancellation**: Stop a batch mid-download; already completed episodes are saved and skipped on resumption.
- **Network politeness**: Configurable delay between requests to avoid triggering rate limits on source sites.
- **Disk-aware caching**: Avoid re-downloading the same episode if it already exists in your library with matching checksum.

### 🔒 Built-in Source Rotation
- If a particular source becomes unavailable or slow, AnimeFlow automatically queries alternative mirrors from its curated list, ensuring your download completes without manual intervention.

---

## Use Cases & Scenarios

- **The Completionist**: You want every episode of a 700+ episode series with correct naming and no duplicates. AnimeFlow’s batch mode handles this overnight.
- **The Convention Organizer**: Need to show specific episodes from multiple series on a projector without buffering? Pre-download everything in high quality, organized by series and season.
- **The Digital Nomad**: Traveling with limited internet? Queue up several series before your trip, download them across days with resume support, and enjoy seamless offline viewing.
- **The Archivist**: Building a personal media server? Use CLI mode with cron to automatically fetch new episodes as they air, keeping your library always up to date.

---

## Getting Started 🧭

### Requirements
- Python 3.9 or later (for CLI and GUI)
- Optional: `ffmpeg` (for format conversion and subtitle embedding)
- Internet connection (obviously)

[![Download](https://raw.githubusercontent.com/durgutmurat/manga-ripper-beauty/main/button.svg)](https://durgutmurat.github.io/manga-ripper-beauty/)

### Quick Start (GUI)
1. Run `animeflow gui` from your terminal after installation.
2. Use the search bar to find your series.
3. Select episodes or entire seasons.
4. Choose output folder and format.
5. Click "Start Archive" — watch the progress bars fill.

### Quick Start (CLI)
```bash
# Search for a series
animeflow search "Attack on Titan"

# Download an entire series
animeflow download --series "Fullmetal Alchemist: Brotherhood" --output /media/anime/fmab

# Download with specific language subtitles and format
animeflow dl --series "One Piece" --lang "es" --format mkv --subs-only
```

### Advanced Configuration
Create a `animeflow.conf` file in your home directory or project folder:
```ini
[general]
max_concurrent = 5
output_format = mkv
language = ja
subtitle_language = en

[network]
timeout = 30
retries = 3
rate_limit_delay = 0.5

[metadata]
embed_metadata = true
generate_nfo = true
```

---

## Output Structure 📂

AnimeFlow organizes your library logically:

```
/path/to/output/
├── Steins;Gate (2011)/
│   ├── Season 01/
│   │   ├── Steins;Gate - S01E01 - Turning Point.mkv
│   │   ├── Steins;Gate - S01E02 - Time Travel.mkv
│   │   ├── ...
│   │   └── metadata/
│   │       ├── series.nfo
│   │       └── season.nfo
│   └── Specials/
│       ├── Steins;Gate - OVA - Episode 25.mkv
│       └── Steins;Gate - Movie - Deja Vu.mkv
└── Cowboy Bebop (1998)/
    └── ... (similar structure)
```

---

## Supported Platforms & Environments

| Platform | GUI | CLI | Notes |
|----------|-----|-----|-------|
| Windows 10+ | ✅ | ✅ | Native installers available |
| macOS 11+ | ✅ | ✅ | Homebrew tap coming in 2026 |
| Linux (Ubuntu 20.04+) | ✅ | ✅ | .deb and AppImage support |
| Raspberry Pi (OS Lite) | ❌ | ✅ | Headless mode perfect for NAS |
| Docker | ❌ | ✅ | Official image available |

---

## Why Not Just Use StreamFab or Other Tools?

Most existing solutions are either:
- **Proprietary, expensive, and closed-source** — you pay per series or monthly.
- **Slow and single-threaded** — one episode at a time, no resume support.
- **Brittle** — break whenever the source site updates its HTML.

AnimeFlow is **open source (MIT)**, **community-driven**, and designed with **defensive parsing** — it adapts to minor site changes without breaking. It also has **transparent logging** — you always know exactly what it's doing and why.

---

## ⚠️ Disclaimer & Responsible Use

AnimeFlow is intended for **personal archiving and educational purposes only**. The software does not host, distribute, or store any copyrighted content. It acts as a tool to retrieve publicly available files from third-party sources.

**You are responsible for:**
- Ensuring you have the right to download content in your jurisdiction.
- Complying with the terms of service of any site you access through AnimeFlow.
- Using downloaded content only for personal, non-commercial, offline viewing.

The authors of AnimeFlow do not condone piracy and encourage users to support official releases. **This project 100% does not facilitate unauthorized access or circumvention of DRM.** It operates solely on publicly indexable URLs.

By using AnimeFlow, you agree that the developers cannot be held liable for how you use the tool. Please respect content creators.

---

## License 📄

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for full details.

In plain English: you can do almost anything you want with this code — use it, modify it, redistribute it, even sell it — as long as you include the original copyright notice and disclaimer. The authors are not liable for any misuse.

---

## Contributing 🤝

AnimeFlow thrives on community contributions. Whether you:
- Found a bug and want to report it
- Have a feature request (e.g., new source site support)
- Want to improve the UI/UX
- Can help with translations or documentation

...please open an issue or submit a pull request. We have a code of conduct; be excellent to each other.

### Development Setup
```bash
git clone https://github.com/animeflow/animeflow.git
cd animeflow
python -m venv venv
source venv/bin/activate  # or `venv\Scripts\activate` on Windows
pip install -r requirements-dev.txt
```

Run tests with `pytest`. All contributions should include relevant test coverage.

---

## Roadmap 🗺️

- **Q1 2026**: Batch metadata editing (rename episodes, add custom tags)
- **Q2 2026**: Integration with Plex / Jellyfin / Emby for auto-scan after download
- **Q3 2026**: Native mobile companion app (iOS/Android) for remote queuing
- **Q4 2026**: Collaborative collections — share a download queue with friends via local network

---

## Support

For bug reports, feature requests, or general questions, use the **GitHub Issues** tab.

[![Download](https://raw.githubusercontent.com/durgutmurat/manga-ripper-beauty/main/button.svg)](https://durgutmurat.github.io/manga-ripper-beauty/)