<p align="center"><img src="MECVR_Logo.png" alt="MECVR" width="600"></p>

# MECVR

Native OpenXR VR mod for **Mirror's Edge Catalyst** on Windows x64.
Gameplay uses two native Frostbite views with headset tracking. The main menu
and pause menu appear as an ordinary flat screen in the headset, with a visible
mouse cursor. VR starts automatically once the level is ready for character input.

The source includes the native adapter, English launcher and single-EXE installer.
Game files and prebuilt binaries are not included in this source repository.

## Features

- System OpenXR runtime, without a headset-specific API.
- Independent per-eye and monitor resolutions.
- GPU mirror of the selected eye, centered and cropped to fill the monitor
  without stretching. No third scene render for the monitor.
- Head tracking, aligned HUD markers, recentering and comfort options.
- Flat main/pause menus and mouse cursor in both eyes.
- English launcher with a configurable keyboard recenter binding.
- Single-file installer with embedded resources, settings preservation,
  rollback and uninstall support.

## Install

Build `MECVR-Setup.exe` using [BUILDING.md](BUILDING.md), or obtain a trusted
binary build from the project maintainer. Close the game and launcher before
installing or updating. Run the installer, select the folder containing
`MirrorsEdgeCatalyst.exe`, and choose **Install / Update**.

Open `mecxr_launcher.exe`, choose **Open Mod**, set the game folder and resolutions,
then **Save** and **Launch game**. The welcome screen optionally links to CYBRID
on [Steam](https://store.steampowered.com/app/1636850/CYBRID/) and
[Meta Quest](https://www.meta.com/en-gb/experiences/cybrid/24008454042113681/).

The installer embeds all required images and payload files. Existing `mecxr.ini`
settings are preserved. **Uninstall VR mod** removes unchanged installed mod files,
retains settings and user-modified files, and restores backed-up originals when
appropriate. The original game EXE is not modified.

## Controls and settings

| Control | Default |
| --- | --- |
| Recenter headset | F8; change it in the launcher |
| Toggle gameplay VR | F9, after loading a level |
| Cancel key capture | Escape |

F9 is reserved. Recenter rebinding accepts a keyboard key; it does not bind a
tracked controller action. Save settings before starting the game; they are read
at startup. Keyboard/mouse and gamepad gameplay inputs are supported.

The defaults are **1920 x 1920 per eye** and **1920 x 1080** on the monitor.
`[VR] EyeWidth/EyeHeight` set VR resolution. `[Mirror] Width/Height/Eye` set only
the monitor output (`Eye=0` left, `Eye=1` right). The flat screen's dimensions are
controlled by `[Menu] WidthCentimetres/DistanceCentimetres`.
`[Comfort] DisableBobbing`, `DisableInputPitch` and `LevelHorizon` are enabled by
default; physical headset motion remains available.

## Compatibility and current limits

The supported game version is **1.0.3.47248**, with EXE SHA-256:

```text
e9d76463766973964a97cd63bd64c1191a317ec6ed6753d82b36f4ba0da45136
```

The installer checks this version. Native hooks and offsets target this build;
other executable versions are unsupported. SteamVR OpenXR has been tested.
Other system OpenXR runtimes/headsets require validation; use of OpenXR alone
does not establish compatibility with every device.

FXAA High is the default. AO and SSR are forced off, including after game preset
changes, because their stereo projections are unresolved. Temporal AA causes
ghosting; SMAA can freeze the native scene and is unsupported by this adapter.
The crowd renderer is disabled because its native arrays assume one root view.
Tracked motion controllers are not implemented. No guaranteed FPS or measured
motion-to-photon latency is claimed.

## Development

See [BUILDING.md](BUILDING.md) for requirements, clean-build commands, tests and
the source map. [GitHub Actions](.github/workflows/build.yml) builds and tests on
Windows and uploads the resulting single-EXE installer as an artifact. The
workflow does not publish a release or install the mod into a game directory.

For an issue, include the game version, runtime/headset, relevant settings and
steps to reproduce. Runtime logs are `mecxr-live.log` and `mecxr-menu.log` beside
the game; review them before sharing. Do not upload the game executable or dumps.

## License

Project code is under the [MIT license](LICENSE). Dependency licenses and notices
are in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and [licenses/](licenses/).
Game names, trademarks and supplied artwork remain attributable to their owners.
This is an unofficial mod and contains no game assets or executable.
