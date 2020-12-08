# assets-for-api-docs

This repo is used to host and serve static assets in support of
[docs.flutter.dev](https://docs.flutter.dev), as well as some manual tests that use
specially-crafted graphics.

Assets committed to this repo and pushed to GitHub are immediately
available for linking and reference.

## URL structure

Reference the assets with this URL structure:

`https://flutter.github.io/assets-for-api-docs/assets/<library>/<asset>`

For example, an image named `app_bar.png` about `AppBar` from the
material library would go in the `assets/material/` directory and be at
`https://flutter.github.io/assets-for-api-docs/assets/material/app_bar.png`.

All asset files should be under the `assets` directory in an appropriate
subdirectory.

## Generation

Images must be code-generated.

To create new images, see the [`packages/diagrams/lib/src/`](./packages/diagrams/lib/src/) directory.

The [`generate.dart`](./bin/generate.dart) script regenerates almost all of existing assets
using the Flutter version you have installed. A small wrapper [`bin/generate.sh`](./bin/generate.sh)
is provided as a convenience.

To limit image generation to certain categories and/or names, run:
```sh
# Filter by category
bin/generate.sh -c cupertino,material
# Filter by name
bin/generate.sh -n basic_material_app,blend_mode
```

`bin/generate.sh -h` lists available arguments.

### Prerequisites

The `generate.dart` script only works on macOS and Linux, because of the supporting apps it needs to
run.

To optimize PNG files, it needs `optipng`, which is available for macOS via Homebrew, and Linux via
apt-get.

To convert animations into mp4 files, it needs `ffmpeg`, available for macOS via Homebrew and Linux
via apt-get.

`flutter`, `dart` (and when using an Android device, `adb`) commands need to be available
in a directory in the `PATH` environment variable. (e.g. PATH=~/<path_to_flutter>/flutter/bin/cache/dart-sdk/bin:~/Android/Sdk/platform-tools:$PATH)

When using an Android device, be sure that the  `adb` command is the same as the one running
as a server (which is often started by your IDE, so use the same `adb` the IDE is running).

## Optimization

Please consider optimization tools for assets.

For PNGs, we recommend `optipng`, using the following command line:

```bash
optipng -zc1-9 -zm1-9 -zs0-3 -f0-5 *.png
```

Be careful about applying this aggressively. In particular, files in
the `assets/tests` directory should not be optimized.

The automatic generation tool will automatically apply optimization to
the assets it generates.

## Origin of third-party content

* `/assets/videos/bee.mp4`: CC0 Creative Commons, from [https://pixabay.com/en/videos/honey-bee-insect-bee-flower-flying-211/](https://pixabay.com/en/videos/honey-bee-insect-bee-flower-flying-211/)
* `/assets/videos/butterfly.mp4`: CC0 Creative Commons, from [https://pixabay.com/en/videos/butterfly-flower-insect-nature-209/](https://pixabay.com/en/videos/butterfly-flower-insect-nature-209/)
* Also see the license information for [images used in the diagrams](packages/diagrams/assets/README.md)
