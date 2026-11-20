# PaganRebuild

A newly written engine for **Ultima VIII: Pagan**, in Rust. It plays the game straight from the original data, without DOSBox, and adds improvements you can switch on and off.

Project page: https://scareglow23.github.io/PaganRebuild/

**No game data is included.** You need your own copy of the game, for example the [Ultima 8 Gold Edition on GOG](https://www.gog.com/en/game/ultima_8_gold_edition).

## Installation

1. Download the zip from [Releases](https://github.com/scareglow23/PaganRebuild/releases).
2. Extract it into the Ultima 8 folder (where `ENGLISH\` is).
3. Run `PaganRebuild\PaganRebuild.exe` (German version: `--lang german`, French: `--lang french`).

Windows 64-bit releases keep saves and settings in `%APPDATA%\pagan`.
On Linux, build from source and run the native executable as shown below.
Saves and settings are kept in `$XDG_DATA_HOME/pagan` (default `~/.local/share/pagan`).

## God Mode

Set `avatar_menu=on` in `settings.ini` or start the game with `--cheat`.
Look at the Avatar, then choose **God Mode: OFF** to turn
protection on. Choose **God Mode: ON** to turn it off again.
The game remembers the choice in `settings.ini`. Ordinary damage affects
the Avatar only while God Mode is off. Scripted story deaths and the
cheat menu's **Kill me** command still work.

## Album music (optional)

PaganRebuild can play the album "Ultima VIII: Pagan - Orchestral Re-Arrangement" instead of the MIDI music. The album is not included:

1. Download the album from [Bandcamp](https://dustinnaegel.bandcamp.com/album/ultima-viii-pagan-orchestral-re-arrangement) as "Ogg Vorbis".
2. Extract the zip into a folder `album` inside the Ultima 8 folder (next to `ENGLISH\`).
3. In the options menu under Sound, set "Music" to "Album".

Original music: Nenad Vugrinec<br>
Arrangement and orchestration: Dustin Naegel<br>
https://dustinnaegel.bandcamp.com/album/ultima-viii-pagan-orchestral-re-arrangement

## Building

Rust (stable) is needed. On Windows the GNU toolchain is used (`stable-x86_64-pc-windows-gnu`).

```
cargo build --release
```

The Windows executable is `target/release/PaganRebuild.exe`. On Linux it is
`target/release/PaganRebuild`. Both look for game data in the folders above the
working directory and the executable. To choose the installation explicitly,
pass the directory containing the language folders. For example:

```sh
./target/release/PaganRebuild --game "$HOME/Games/u8gog"
```

On Linux, building requires a C linker, `pkg-config`, ALSA and libudev
development files. On Arch Linux, use `base-devel`, `alsa-lib` and
`systemd-libs`. The game runs under Wayland or X11 and tries Vulkan first,
then GLES. On Intel Mesa, the relevant driver packages are `vulkan-intel`
and `mesa`. Use `WGPU_BACKEND=gl` to select GLES explicitly.

Linux MIDI playback uses an SF2 SoundFont. Place one in the user folder's
`soundfonts` subdirectory or in a `soundfonts` folder next to the executable.
The optional album works on Linux as well.

Run `PaganRebuild --help` for all command-line options. To run tests against a
separate game installation, set `PAGAN_TEST_GAME` to the same directory you
would pass to `--game`.

## Credits

Based on the work of ScummVM (formerly Pentagram), https://www.scummvm.org/.<br>
SoundFont: GeneralUser GS by S. Christian Collins, https://www.schristiancollins.com/generaluser.php.

Ultima VIII: Pagan (c) 1994 Origin Systems / Electronic Arts. Fan project, not affiliated with Electronic Arts or Origin Systems.

PaganRebuild is developed with the help of Claude Code (Anthropic).

## License

GPL-3.0-or-later, see [LICENSE](LICENSE).
