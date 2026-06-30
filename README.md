# octron-forge

[![Pixi Badge](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/prefix-dev/pixi/main/assets/badge/v0.json)](https://pixi.sh)
[![prefix.dev channel](https://img.shields.io/badge/prefix.dev-octron-3f5cc7?logo=condaforge&logoColor=white)](https://prefix.dev/channels/octron)
[![Build and upload](https://github.com/roaldarbol/octron-forge/actions/workflows/build-and-upload.yml/badge.svg)](https://github.com/roaldarbol/octron-forge/actions/workflows/build-and-upload.yml)
[![License: GPL-3.0](https://img.shields.io/badge/License-GPL%203.0--or--later-blue.svg)](https://github.com/OCTRON-tracking/OCTRON-GUI/blob/main/LICENSE)

Conda package recipes for [**OCTRON**](https://github.com/OCTRON-tracking/OCTRON-GUI) — a [napari](https://napari.org)-based pipeline for segmentation, detection, and tracking of animals in behavioral setups — and the dependencies it needs that aren't available on conda-forge.

Packages are built with [`rattler-build`](https://rattler.build) and published to the [`octron` channel on prefix.dev](https://prefix.dev/channels/octron).

## Installation

OCTRON and its bundled dependencies live on the `octron` channel; everything else resolves from `conda-forge`. Always pass both channels.

With [pixi](https://pixi.sh):

```bash
pixi global install octron -c https://prefix.dev/octron -c conda-forge
```

Or into a pixi project:

```bash
pixi add octron -c https://prefix.dev/octron -c conda-forge
```

With conda / mamba:

```bash
conda create -n octron -c https://prefix.dev/octron -c conda-forge octron
```

Once installed, launch the GUI from your application menu (a desktop/Start-menu shortcut is created on install) or from a terminal:

```bash
octron-gui
```

## Recipes

| Recipe | Published package | Purpose |
| --- | --- | --- |
| [`octron`](recipes/octron) | `octron` | The OCTRON GUI (main application) |
| [`sam-2`](recipes/sam-2) | `sam2-octron` | Segment Anything 2 — segmentation backbone |
| [`napari-pyav`](recipes/napari-pyav) | `napari-pyav-octron` | PyAV-based video reader for napari |
| [`boxmot`](recipes/boxmot) | `boxmot-octron` | Multi-object tracking |
| [`clip`](recipes/clip) | `clip-octron` | CLIP embeddings |
| [`cotracker`](recipes/cotracker) | `cotracker-octron` | CoTracker point tracking |

## Building locally

This repo is a pixi workspace with `rattler-build` available:

```bash
pixi install
pixi run rattler-build build \
  --recipe recipes/octron/recipe.yaml \
  --channel https://prefix.dev/octron \
  --channel conda-forge
```

## Automation

- **PR builds** — opening a PR that touches a recipe builds the affected package(s) to catch errors before merge ([`build.yml`](.github/workflows/build.yml)).
- **Build & upload** — merges to `main` rebuild changed recipes and upload them to the `octron` channel ([`build-and-upload.yml`](.github/workflows/build-and-upload.yml)).
- **Recipe updates** — a weekly job watches the upstream [OCTRON-GUI](https://github.com/OCTRON-tracking/OCTRON-GUI) repo and opens a PR bumping the `octron` recipe (version, sha256, build number) when a new release appears ([`update-octron.yml`](.github/workflows/update-octron.yml)). Dependency pins are left for manual review.

## License

OCTRON is licensed under [GPL-3.0-or-later](https://github.com/OCTRON-tracking/OCTRON-GUI/blob/main/LICENSE). The recipes in this repository are maintained by [@roaldarbol](https://github.com/roaldarbol) and [@horsto](https://github.com/horsto).
