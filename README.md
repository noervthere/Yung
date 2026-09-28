<div align="center">

<img src="assets/readme-now-playing.png" alt="Yung playing a song, the cover in a flower shape ringed by the visualizer" width="100%">

<a href="https://buymeacoffee.com/e_gurl">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Support Yung on Buy Me a Coffee" width="217" height="60">
</a>

# Yung

**YouTube Music, your music files, and your music server. Native on Yen Linux.**

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Yen Linux](https://img.shields.io/badge/platform-Yen_Linux-blue.svg)
![Qt 6](https://img.shields.io/badge/built_with-Qt_6-41CD52.svg)

A minimal Material 3 player built with C++ and Qt Quick, designed for Yen and Wayland.

[Install](#install) · [Features](#features) · [Development](#development)

</div>

## Features

- **YouTube Music**: search songs, albums, artists and playlists; play audio without an embedded browser or ad interface, at standard quality or a data saver setting.
- **Navidrome / Subsonic**: browse and search your server, play original or transcoded audio, edit server playlists, rate songs, sync favorites and listening history, and display server lyrics.
- **Jellyfin**: browse music libraries, albums, artists and genres; search, stream original or transcoded audio, manage permitted server playlists, sync favorites and display synchronized lyrics.
- **Apple Music through Cider**: browse your Apple Music library, search Apple's catalogue and play it through [Cider](https://cider.sh), with Yung's queue, lyrics, history and animated covers.
- **Your music**: import FLAC, MP3 and other supported audio files or folders; browse albums and artists, search paths and group songs by folder. Mix local and YouTube songs in the same playlists.
- **Animated artwork**: local animated covers and automatic online covers for matching YouTube songs, shared across the player, immersive view and mini player; lists use still covers.
- **Appearance**: light and dark themes, a pickable Material accent color, artwork-derived color, an ambient cover backdrop, density and per-view layouts.
- **Lyrics**: synchronized lyrics, an immersive view, optional poster-style lines, timing adjustments, LRC import, seek previews and search with jump-to-line playback.
- **Offline**: songs you have played are kept on disk under a limit you set, so a replay starts at once and needs no network.
- **Library tools**: likes, listening history, smart mixes, custom smart playlists, M3U playlist import and export, custom playlist covers, playlist cleanup, multi-selection, drag reordering and Undo.
- **Playback controls**: mini player, queue editing with source headings, an immersive up-next carousel, volume normalization, shuffle, repeat, sleep timer, playback speed and audio-device selection.
- **Keyboard and assistive use**: every control takes focus and shows it, sections are marked as headings, and colors are solved to keep 4.5:1 contrast in both themes and at either contrast setting.
- **Desktop integration**: media keys through MPRIS, optional notifications, light/dark themes and Noctalia palette support.

Native rendering and bounded artwork caches keep Yung lightweight. Animated covers share one additional decoder, released when the player is hidden. Animations can be disabled in Settings.

## Install

### Yen Linux

Install the build and runtime dependencies:

```bash
sudo pacman -S --needed git base-devel cmake ninja python nodejs ffmpeg qt6-base qt6-declarative qt6-multimedia qt6-svg qt6-wayland qt6-imageformats
```

Download and install Yung:

```bash
git clone https://github.com/noervthere/Yung.git
cd Yung
./scripts/install.sh
```

Open **Yung** from your application menu, or run:

```bash
~/.local/bin/yung
```

Installation is per-user in `~/.local`; do not run the install script with `sudo`. Python dependencies are installed in an isolated environment. Internet access is needed during installation and for YouTube access.

### Other Linux distributions

Install the equivalent development packages for **Qt 6.8+** (Core, Gui, Quick, Qml, QuickControls2, Multimedia, Network, DBus, Svg and Wayland), a C++20 compiler, CMake 3.24+, Ninja, Python 3 with `venv`, Node.js, FFmpeg and development headers for libpulse.

Then build from the checkout as described in [Development](#development).

Yung uses Google Sans Flex when installed and otherwise falls back to a system font. Noctalia is optional.

## Getting started

### Music library

Search for music or paste a YouTube song or playlist link. Use **Library → Local files → +** to add files, or **Folders → Add folder…** for a whole music folder. Enter its absolute path (or `~/Music`).

In **Local files**, open **Find and sort songs → Folder** to group songs by their parent directory, with natural filename order inside each group. The filter also searches folder paths.

With a song list focused, start typing to jump to the first matching title, or artist when no title matches. The search refines as you type and clears after a short pause. Turn it off with **Settings → Library → Typing jump**.

Create an automatic playlist from **Library → Playlists → Smart playlist**. Combine artist, title, album, release-year range, length range, source, liked status and last-played rules over your saved songs.

**Local files → Albums / Artists** groups imported music by its tags. Albums use album-artist tags when present, with disc and track order preserved. Use **Rescan** after upgrading to refresh tags or rebuild artwork.

**Library → Playlists → Import M3U** reads an `.m3u` or `.m3u8` file, imports the audio it names and saves it as a playlist. Relative entries resolve against the playlist file's own folder. A playlist whose path is given as `~/music/list.m3u8` refers to files in `~/music/`.

In a playlist's menu, choose **Change cover…** to crop a PNG, JPEG or WebP. Yung saves a 512px copy; the original stays untouched. **Restore cover collage** returns to automatic artwork.

### Artwork and appearance

Home, Search and Library sit in a capsule at the top of the window, with the mini player and Settings at its right. Below 600px the capsule gives up the centre and the bar spans the window instead, so navigation stays reachable on phones.

On first run Yung offers a three-step setup: theme and accent color, a music folder, and the page to open on. Every step can be skipped, and each control also lives in Settings.

Open **Home → Customize Home** to reorder or hide sections; **Reset layout** restores them. **Settings → Library → Start page** chooses Home, Local, Server or Liked for future launches. Direct links to Local, Library, Search and a server's root open that view, and skip the Start page if one is set.

**Settings → Appearance → Current view layout** saves a density override for the current view. Local album/artist browsers and the playlist overview also offer Grid / List. Choose Default density in Settings and use these per-view controls to vary it.

**Settings → Appearance → Density** switches between comfortable and compact track rows and album grids without changing font size. Density changes animate when motion is enabled. Opening an album from a compact row, or search from a list, expands to comfortable; close it and it returns to the saved density.

For animated artwork, place a **GIF, animated WebP, MP4 or WebM** beside your music, named `cover`, `folder`, `front` or `artwork` (for example, `cover.mp4`). A matching song filename, such as `Song.gif`, takes precedence over `cover.gif` in the same folder.

A song that is a music video or an upload has a video frame for a cover rather than album art. Wherever that cover is drawn larger than a list row, Yung asks YouTube for the 1280 × 720 frame and keeps it in cache.

**Settings → Appearance → Album covers for music videos** goes further and looks for the album's own cover on Apple Music's public pages, using the same unofficial, best-effort match as animated online covers. This is a background task and does not wait.

For YouTube songs, **Online animated covers** looks for a matching album on Apple Music's public pages. This unofficial, best-effort lookup needs no account; it sends the song's title and artist to Apple's web search, and picks the first match. Opt in to allow network requests for this purpose.

Open **Settings → Appearance → Current artwork** to preview the current cover, view its source album, retry a match, disable animation for that song or choose a local GIF, WebP, MP4 or WebM. Local choices persist until a next song.

**Settings → Appearance → Use artwork accent** colors controls from the current cover. It is off by default; desktop surfaces and Noctalia integration are preserved. Monochrome or missing covers use the chosen Material source color instead.

**Settings → Appearance → Accent color** picks a Material source color for buttons, highlights and progress. Yung solves each seed against the current surfaces, so the resulting color always clears 4.5:1 contrast in both themes and at either contrast setting.

**Settings → Appearance → Ambient artwork backdrop** draws the current cover, softened and dimmed, behind Home, the immersive player and the Now playing panel. Home has no cover of its own, so it uses a fallback when none is available; disable this control for a plain surface.

The artwork controls also offer **Fit / Fill**, remembered per album where album metadata is available, otherwise per song. Immersive artwork requests a display-sized still cover up to 1600px; source covers are cached and reused.

Click album or immersive artwork to inspect the full cover. Use the wheel or + / − to zoom, 0 to reset, and Escape to close. The viewer uses available source detail, capped at 1600px. You can also zoom a mini-player cover by clicking it.

### Playback and shortcuts

Press **F11** for immersive playback. The **…** menu selects Artwork, Lyrics, Split, Sing along or Visualizer; **Ctrl+L** opens the queue. Visualizer cuts the cover to one of twelve round Material shapes and animates its edges and centre to the audio.

The same **���** menu offers **Up next covers**: a carousel of the queue below the player, with the playing track centered and large and the rest peeking either side. Scrolling snaps to a cover and plays that song.

**Settings → Playback → Crossfade** overlaps the end of one song with the beginning of the next, by up to twelve seconds. Two pairs are joined rather than blended: two tracks of the same album, before and after a fade; a track followed by a live or remix version; or a live set split across tracks.

The sleep timer can stop at the **end of the queue** as well as after a set time or the current track. It is offered only when the queue can actually finish, so it is unavailable while shuffle or repeat-all is on.

**Settings → Playback → Resume long recordings** returns to where you left a recording of 20 minutes or more: mixes, sets and live shows. The mark is written when you pause or move on, dropped once you reach the end or skip past it.

A song's menu offers **Adjust volume…** to trim that one song by up to 12 dB. The trim is kept for that song, applies whether or not volume normalization is on, and appears in **Track details**.

**Settings → Playback → Fade out before sleep** lowers the audio over the last 30 seconds of a timed or end-of-track sleep timer. Your chosen volume stays saved and is restored when the timer ends.

Drag a queue row sideways to remove it; the row lifts into its own color while you carry it, and the gap it will fall into is drawn as you drag it up or down. Undo restores it.

Queue headings distinguish songs added manually, collection tracks and autoplay recommendations when their origin is known. These labels preserve playback order, including after dragging songs. Older versions are still visible: reorder them, if you like, or they fade when a next addition arrives.

Hold **Shift while dragging the seek bar** for fine seeking; the new position applies when you release. **Shift+Left / Right** seeks by 100ms. Escape cancels a fine drag. The mouse wheel over the seek bar seeks by 10s; the arrow keys seek by 5s.

The mini player can be pinned above other windows wherever the desktop allows a window to ask for that. Wayland has no protocol for it, so the control is not offered in a Wayland session; on Hyprland and sway you can pin it yourself:

```
windowrulev2 = float, title:^(Yung · Mini player)$
windowrulev2 = pin, title:^(Yung · Mini player)$
```

Click the volume icon for a slider and an exact percentage. Enter a value from 0 to 100 and press Enter or Apply. This works in the main, mini and immersive players. In the main and immersive players, hold Shift and scroll the wheel over the volume icon to adjust it.

**Settings → Appearance → Poster-style lyrics** sets the line being sung the way Google Sans Flex sets a poster: each word takes its own weight, width, roundness and slant, and each row is stretched to fill the width. It is off by default; turn it on to match your font.

Timed lyrics show a countdown during intros and explicit gaps of at least five seconds. Yung uses supplied line boundaries or blank timed lines; it does not infer instrumental passages from a long lyric gap.

The queue shows remaining time and a finish estimate during uninterrupted playback. Unknown durations, random shuffle, repeat, autoplay or a sleep timer can make a finish estimate unavailable.

Album pages show the artist, release year when available, track count and duration, with disc headings when the source supplies disc numbers. Drag the lyrics/queue divider to resize the panel; double-click to hide the lyrics panel.

Press **Ctrl+Shift+P** for quick actions, saved playlists and audio outputs. Type to filter, use the arrow keys, then press Enter.

**Listening sessions** in Settings or Quick Actions save your queue, song position, speed, shuffle, repeat and autoplay settings. Resume asks before replacing the current queue. Sessions can be renamed or deleted in Settings.

The arrow beside the player's volume controls opens an audio-output picker. It remains available in narrow windows.

**Settings → Playback → Volume normalization** evens out loudness between recordings. ReplayGain and R128 tags are read when a file is imported; everything else, including YouTube and server audio, is analyzed on first play.

**Pause when audio output disconnects** is optional. Yung pauses when the selected device disappears; wired headphone-port detection uses `pactl` from `libpulse`. Reconnecting does not automatically resume.

**Track details** shows playback codec, bitrate and decoded sample rate/channels when reported by the decoder. Local file metadata is labeled separately. Missing values are omitted.

**Settings** groups controls into Appearance, Playback, Library, Connections, and Privacy & data. Search finds controls across all categories. Narrow windows use a category selector.

Open a song's menu to queue it, like it or add it to a playlist. Local playlist additions skip duplicates and can be undone. Views remember their filter, sort and scroll position during the session.

| Shortcut | Action |
| --- | --- |
| Space | Play / pause |
| Ctrl+F | Focus search |
| Ctrl+Shift+P | Quick actions |
| Ctrl+J | Show the playing song in the queue |
| ? / F1 | Keyboard shortcut reference (outside text fields) |
| Ctrl+M | Toggle mini player |
| F11 | Toggle immersive player |
| 0 – 9 | Jump to that tenth of the track |
| Ctrl+A | Select songs in the focused list |
| Escape | Close the current view or clear selection |

### Connect a music server

Open **Settings → Connections → Music server** and choose **Subsonic** (including Navidrome) or **Jellyfin**, and enter your server address, username and password. Use the server root, including any port, without a trailing slash.

Open **Library → Music server** to browse. The search bar on that page searches your server. The server menu offers library selection and playlist creation. Permitted playlists support renaming, song removal, liked/unliked toggles, and reordering.

Local playlists can mix YouTube, local files and server songs. Server playlists accept songs from that server only. One server account can be connected at a time. Server lyrics use synchronized lyrics from the server when available.

**Remember in desktop keyring** uses `secret-tool` (the `libsecret` package on Arch) and a running Secret Service provider. If the keyring is unavailable, the connection works for the current session.

Connection settings include audio quality and server listening history. Original audio is buffered on disk before playback, with a 512 MiB limit per song; choose a lower bitrate for very large files. Prefer original quality unless bandwidth is limited or the server transcodes.

Tested against Navidrome 0.63.2 and Jellyfin 10.11.11 / 12.0. Other servers must support Subsonic 1.16.1 token authentication and JSON responses. OpenSubsonic lyrics and form POST are detected when available.

### Connect Apple Music through Cider

Apple streams Apple Music only to its own players, so Yung plays it through Cider, the Apple Music client, which needs its own copy and your Apple Music subscription. In Cider, open **Settings → Connectivity** and switch on the internal server, then return to Yung.

**Library → Music server** then lists your Apple Music albums, artists and playlists, **Discover** shows your country's song chart, and the search bar searches Apple's catalogue. Cider must stay open while Yung is in use; close Yung first to avoid warnings.

The sound comes out of Cider, so Yung's playback speed, crossfade and loudness levelling do not apply to Apple Music songs, and the volume slider sets Cider's volume. The visualizer, the playing bars and immersive playback reflect Cider's output.

### Accounts and saved data

**Settings → Connections → YouTube → Streaming quality** chooses what a song costs to download. Standard takes the best stream YouTube offers, which is Opus at about 130 kbps. Data saver caps it at 100 kbps.

YouTube browsing is anonymous. YouTube likes, local playlists and local history are stored locally and **do not sync with your Google account**. Settings offers library JSON import/export; audio files are not included.

For streams requiring sign-in, Settings can import a user-selected Netscape-format cookie file. Yung does not read your browser profile. Cookies can be removed in Settings.

**Settings → Privacy & data → Keep played songs** keeps the audio Yung has already fetched. Yung buffers a whole song to disk before playing it either way; this keeps that file instead of handing it off to the system for deletion.

Library data is stored in `~/.local/share/Yung/yung/`, settings in `~/.config/Yung/`, and cache in `~/.cache/Yung/yung/`. Standard XDG directory overrides are respected. Yung has no analytics or telemetry.

### Troubleshooting

Playback depends on YouTube availability, region and network conditions. Yung buffers audio before playing, so starting a song can take a moment. It does not remove sponsor segments embedded in recordings.

If YouTube playback stops working after an upstream change, update the resolver:

```bash
~/.local/lib/yung/runtime/bin/python -m pip install --upgrade 'yt-dlp[default]' ytmusicapi
```

To update Yung, quit the player, then run `git pull` and `./scripts/install.sh` from this checkout. To uninstall, run `./scripts/uninstall.sh`; your library and settings are kept.

## Development

Build and run from the checkout:

```bash
./scripts/setup.sh
./scripts/build.sh
./scripts/run.sh
```

Run automated tests:

```bash
./scripts/test.sh
./scripts/verify.sh --offline
```

The offline suite includes immersive-player checks at normal and high DPI, plus process-restart checks for saved layout preferences. To run just these checks against a build configured with `-DYUNG_DIAGNOSTICS=ON`:

```bash
python3 tests/immersive_regression.py --binary /path/to/diagnostics/yung --output verification/immersive
```

Use a new output directory. These checks run offscreen with generated silent music and isolated settings.

The full integration suite is `./scripts/verify.sh`. It needs network access, a working audio session, Google Sans Flex, Qt Test, `qdbus6` and `dbus-run-session` (`qt6-tools` and `dbus` provide the commands).

Reports and screenshots are written to the ignored `verification/` directory. Do not attach raw logs or cookie files to issues; playback logs may contain signed media URLs. The Git allowlist keeps build artifacts and local dependencies out of version control.

To test the server integration, build the test targets and provide a Navidrome executable:

```bash
./scripts/test.sh
python3 tests/navidrome_integration.py \
  --navidrome /path/to/navidrome \
  --test-binary build-tests/yung-subsonic-tests \
  --output verification/navidrome
```

The script starts a loopback-only server, creates a temporary account and 105 generated audio fixtures, and tests browsing, playback, seeking, lyrics, playlist edits, ratings, favorites, queue restoration and history sync.

To check the Cider integration against your own Cider, with Cider open and nothing playing in it, pass the token from its Connectivity settings. It searches Apple Music, plays a song for three seconds and checks the queue:

```bash
YUNG_CIDER_LIVE_TOKEN=... ctest --test-dir build-tests -R cider --output-on-failure
```

To test Jellyfin with generated music and disposable accounts:

```bash
python3 tests/jellyfin_integration.py \
  --server-binary /path/to/jellyfin \
  --test-binary build-tests/yung-jellyfin-tests \
  --output verification/jellyfin
```

The server binds to loopback only and stops after testing. Test data and credentials stay in the private output directory; remove it when finished. Add `--ui-binary /path/to/yung` for rendered UI checks.

## License

[MIT](LICENSE). Material Symbols are licensed under Apache-2.0; see [NOTICE](NOTICE) for third-party acknowledgments. Yung is an independent project and is not affiliated with Google or YouTube.
