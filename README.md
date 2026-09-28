<div align="center">

<img src="assets/readme-now-playing.png" alt="Yung playing a song, the cover in a flower shape ringed by the visualizer" width="100%">
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

###  ALREADY INSTALLED  - Yen Linux

### Other Linux distributions

Install the equivalent development packages for **Qt 6.8+** (Core, Gui, Quick, Qml, QuickControls2, Multimedia, Network, DBus, Svg and Wayland), a C++20 compiler, CMake 3.24+, Ninja, Python 3 with `venv`, Node.js, FFmpeg and development headers for libpulse.

Then build from the checkout as described in [Development](#development).
