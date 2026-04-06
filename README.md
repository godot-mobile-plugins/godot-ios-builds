# godot-ios-builds

Pre-built iOS static libraries and generated header files from [Godot Game Engine](https://godotengine.org) builds, published automatically for every Godot release.

## What's in each release

Each release corresponds to a tag from [godotengine/godot-builds](https://github.com/godotengine/godot-builds) and follows the same naming convention — `<version>-<flavor>`, for example `4.6.2-rc2` or `4.5.2-stable`.

Five ZIP archives are attached to every release:

| Archive | Contents |
|---|---|
| `godot-headers-<version>-<flavor>.zip` | Every `*.glsl`, `*.h`, `*.hh`, `*.hpp`, `*.inc`, and `*.inl` file produced by the iOS build. Useful for native plugins that need to compile against Godot's internal API without building the engine from source. |
| `godot-ios-device-debug-<version>-<flavor>.zip` | `libgodot.ios.template_debug.arm64.a` — debug static library for physical iOS devices. |
| `godot-ios-device-release-<version>-<flavor>.zip` | `libgodot.ios.template_release.arm64.a` — release static library for physical iOS devices. |
| `godot-ios-simulator-debug-<version>-<flavor>.zip` | `libgodot.ios.template_debug.arm64.simulator.a` — debug static library for the iOS Simulator. |
| `godot-ios-simulator-release-<version>-<flavor>.zip` | `libgodot.ios.template_release.arm64.simulator.a` — release static library for the iOS Simulator. |

All archives preserve the `bin/` directory path from the Godot source tree.

## Using the archives

### Headers

1. Go to the [Releases](https://github.com/godot-mobile-plugins/godot-ios-builds/releases) page and download `godot-headers-<version>-<flavor>.zip` for the Godot version you are targeting.
2. Extract the archive and add the header paths to your Xcode project or build system's include search paths.

### Static libraries

1. Download the archive(s) you need for your target (device and/or simulator, debug and/or release).
2. Extract the archive and locate the `.a` file inside the `bin/` directory.
3. Add the static library to your Xcode project's **Link Binary With Libraries** build phase.
4. If you need a single library that runs on both physical devices and the simulator, combine the two `arm64` slices into an XCFramework using `xcodebuild -create-xcframework`.

## Release schedule

New releases are checked for and created automatically twice a week — every **Thursday** and **Sunday** at 04:00 UTC — via the [Archive Godot iOS Builds](.github/workflows/archive-ios-builds.yml) workflow. The workflow compares the 10 most recent releases in `godotengine/godot-builds` against this repository and builds any that are missing.

A release can also be triggered manually for a specific version from the [Actions](https://github.com/godot-mobile-plugins/godot-ios-builds/actions) tab.

## Related

- [godotengine/godot](https://github.com/godotengine/godot) — Godot engine source
- [godotengine/godot-builds](https://github.com/godotengine/godot-builds) — official Godot release tags
- [ActionCommons/build-godot](https://github.com/ActionCommons/build-godot) — the GitHub Action used to produce these archives
