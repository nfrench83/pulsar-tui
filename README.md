✦ Pulsar TUI
A high-performance modern terminal media and torrent streaming client written in Rust.

Rust
Rust
 
License: MIT
License: MIT
 
Platform
Platform
 
Media Players
Media Players

Stream movies, television series, anime, trailers, and torrents directly in your terminal with zero bloat, instant hardware-accelerated playback, sub-millisecond A/V synchronization, and universal addon extension support.

🌟 Highlights & Key Features
🚀 Ultra-Fast Embedded Streaming Engine:
Integrated Node.js torrent streaming server (server.js) with sequential piece prioritization.
Adaptive Swarm Choke Management: Proven seeders (downloaded > 0) are protected from premature disconnects during unchoke rotations.
Multi-tiered streaming profiles: Ultra Fast (120 peers, uncapped line speed, 10GB cache), Fast, Default, and Soft.
🎬 Dual Media Player Support (MPV & VLC):
Seamlessly toggle between MPV and VLC at any time by pressing [m] in the Cloud Account tab ([5]).
Optimized network caching buffers (--demuxer-max-bytes=256MiB for MPV, --network-caching=5000 for VLC).
Graceful fallback to MPV if VLC is selected on a system without VLC installed.
🔊 Sub-Millisecond Audio & Video Synchronization:
30-Second Demuxer Pre-Caching (--demuxer-readahead-secs=30): Decodes and queues audio/video ahead of time in RAM so transient torrent buffer dips never starve the audio driver.
Active Drift Recovery (--autosync=30): Automatically measures and corrects A/V delay within 1–2 seconds if a network hitch occurs.
Master Audio Clock Slaving (--video-sync=audio): Keeps video locked to audio presentation timestamps without pitch distortion (--audio-pitch-correction=yes).
📺 3-Panel Series Navigation with TVMaze Scene Alignment:
Column 1: All seasons with episode tallies.
Column 2: Episode guide with canonical titles, episode numbers, and air dates.
Column 3: Real-time stream and torrent scrapes ranked by seeders, resolution, and source.
Canonical Episode Alignment: Automatically cross-references TVMaze to align episode ordering with scene torrent releases (eliminating inversions on legacy air-date shows like South Park S02E03 vs S02E04).
🧩 Universal Extension & Addon Ecosystem:
Full compatibility with Stremio v3 protocol addon manifests.
Pre-configured and community support for Torrentio, Cinemeta, MediaFusion, Orion, TheMovieDatabase (TMDB), Anime Kitsu, OpenSubtitles v3, and WatchHub.
Instant Debrid streaming support (Real-Debrid, Torbox, AllDebrid) for cached high-speed HTTP streams without local P2P swarm overhead.
📚 Local & Cloud Watchlist / Continue Watching:
Sync cloud profile watch history, or bookmark titles locally with a single keystroke ([b]).
Automatic resume points and watched status indicators ([w]).
📦 Installation Across Linux Distributions
Pre-built binaries, distribution packages, and checksums are located in 
Work/dist/
.

Option 1: Standalone Linux Installer (Recommended)
Run the universal installer script:

bash

bash ~/Work/install-pulsar-tui.sh
Installs binary to ~/.local/bin/pulsar-tui (symlinked as pulsar and stremio-tui).
Installs streaming engine to ~/.local/share/pulsar-tui/server.js.
Installs desktop launcher (pulsar-tui.desktop) and vector/raster icons to system hicolor theme.
Option 2: Universal Portable Tarball (.tar.gz)
Works out-of-the-box on any Linux distribution (Ubuntu, Debian, Fedora, Arch, openSUSE, Alpine, Void):

bash

# 1. Extract package
tar -xzf pulsar-tui-v0.1.0-linux-x86_64.tar.gz
cd pulsar-tui-v0.1.0-linux-x86_64
# 2. Run local installer
./install.sh
# Or run directly without installation:
./pulsar-tui
Option 3: Arch Linux / Manjaro / EndeavourOS (.pkg.tar.zst)
Install directly with pacman:

bash

sudo pacman -U pulsar-tui-bin-0.1.0-1-x86_64.pkg.tar.zst
Or build locally with makepkg:

bash

cd packages/arch
makepkg -si
Option 4: Debian / Ubuntu / Linux Mint / Pop!_OS (.deb)
Install with apt (automatically resolves recommended dependencies):

bash

sudo apt install ./pulsar-tui_0.1.0-1_amd64.deb
Or with dpkg:

bash

sudo dpkg -i pulsar-tui_0.1.0-1_amd64.deb
Option 5: Fedora / RHEL / openSUSE (.rpm)
Install with dnf or rpm:

bash

sudo dnf install ./pulsar-tui-0.1.0-1.x86_64.rpm
⚡ Recommended Dependencies
While Pulsar TUI is a self-contained Rust binary with an embedded streaming server, installing one or both media players is recommended:

MPV: sudo pacman -S mpv / sudo apt install mpv / sudo dnf install mpv
VLC: sudo pacman -S vlc / sudo apt install vlc / sudo dnf install vlc
Node.js: node runtime for the local torrent streaming engine.
Clipboard Utility: wl-clipboard (Wayland) or xclip (X11) for seamless Ctrl+V pasting.
⌨️ Comprehensive Keybindings Reference
Global Navigation & Views
Key	Action
[1]	Switch to Discover view (catalogs, genres, trending)
[2]	Switch to Library view (Continue Watching, Watchlist)
[3] or [/]	Switch to Search view (search across all addons)
[4]	Open Addon Store (Installed, Featured, Community)
[5]	Open Cloud Account & Engine (Profiles, Player, Login)
[6] or [?]	Show Help & Keybindings cheatsheet
[q] or [Ctrl+C]	Quit Pulsar TUI
Browsing & Playback
Key	Action
[Tab]	Cycle panel focus (Catalogs / Items / Seasons / Episodes / Streams)
[Enter]	Open series details / Open movie streams / Focus panel
[p]	Quick Play: Scrape and immediately play best stream
[i]	View full synopsis, cast, metadata, and background
[g]	Filter Discover catalog by Genre
[n]	Load next page of 50 titles in catalog
[b] / [l]	Quick bookmark / remove title from Library
[w]	Toggle watched / unwatched in Library
[d]	Delete title from Library
[s]	Toggle stream sorting (Seeders vs Quality)
[t]	Play official trailer
[c]	Copy stream URL or Magnet link to clipboard
[Ctrl+V]	Paste clipboard text into active input field
[Ctrl+U]	Clear active input field
[Esc]	Close modal / return to main view
Engine & Player Configuration (Account Tab [5])
Key	Action
[m]	Toggle Media Player: Cycle between MPV and VLC
[t]	Cycle Torrent Profile: Ultra Fast → Fast → Default → Soft
[s]	Sync addons from Cloud account
[l]	Sync saved library from Cloud account
[o]	Log out of Cloud account
In-Player Hotkeys (A/V Synchronization & Subtitles)
Action	MPV	VLC
Adjust Audio Delay (A/V Sync)	Ctrl + + / Ctrl + - (±100ms)	j / k (±50ms)
Adjust Subtitle Delay	z / Z (±100ms)	g / h (±50ms)
Adjust Playback Speed	[ / ]	[ / ]
Cycle Audio Tracks	#	b
Cycle Subtitles	v	v
🔧 Configuration & File Paths
Configuration files are stored in ~/.config/pulsar-tui/config.json. Any legacy configurations from ~/.config/stremio-tui/ are automatically migrated upon first launch.

json

{
  "installed_addons": [...],
  "preferred_player": "mpv",
  "stremio_engine_url": "http://127.0.0.1:11470",
  "auto_play_highest_quality": false,
  "torrent_profile": "UltraFast",
  "stremio_auth_key": null,
  "stremio_user_email": null,
  "library": [...]
}
🧹 Uninstallation
To completely remove Pulsar TUI from your system:

bash

bash ~/Work/install-pulsar-tui.sh --uninstall
📄 License
Pulsar TUI is distributed under the MIT License.
