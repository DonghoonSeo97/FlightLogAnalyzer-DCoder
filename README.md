# DCoder V4.8

> English | [한국어](README.ko.md)

**DCoder** is a local-first desktop workbench for flight-log and experimental time-series analysis, developed and maintained by **[Company Name / Engineering Team]**.

It is designed for engineers who need to load logs quickly, inspect signals, create derived channels, compare time ranges, and export reusable analysis outputs without depending on a cloud platform or a full engineering IDE.

## About this repository

This repository contains the **DCoder V4.8** desktop application built with **Python** and **PySide6**.

DCoder is positioned as an **analysis workbench**, not as:
- a GCS for mission upload, vehicle control, or firmware flashing,
- a cloud data platform for organization-wide indexing and collaboration,
- or a general-purpose engineering IDE.

Its core goal is simple:
**open data fast → isolate the right interval → inspect the cause → save and reproduce the session**.

## Key capabilities

### Core workflow
- Load offline logs and experimental datasets
- Browse available fields and build plot workspaces
- Create multiple figures with overlay and stack plotting
- Synchronize plots on a shared time base
- Save and restore analysis sessions
- Export selected results for downstream workflows

### Analysis-oriented features
- Segment-based workflow for interval selection and comparison
- Derived signal generation
- Quick conversion tools such as quaternion-to-Euler
- Analysis Lab with built-in and add-on function execution
- Function execution history and reusable presets

### Supported and expandable inputs
- CSV
- ArduPilot BIN
- PX4 ULog
- Crazyflie logs
- ROS 2 bag workflows
- MCAP
- Telemetry-oriented extension points

Some input formats depend on optional parser packages. See the installation section below.

## Why DCoder

DCoder aims to combine strengths that are often split across multiple tools:
- the immediacy of field log inspection,
- the speed of time-series plotting tools,
- the reproducibility of session-based analysis,
- and the practicality of a local desktop workflow.

The product philosophy is:
- **local-first**,
- **segment-first**,
- **analysis-centered**,
- **extensible by developers**,
- **repeatable across sessions**.

## Screenshots

Add screenshots or GIFs here before public release.

Recommended assets:
- Main workspace view
- Field selection and plotting workflow
- Analysis Lab
- Segment Manager
- 3D trajectory view

## Installation

### Option 1. Use the GitHub Release package

For most users, download the latest Windows release asset from the **Releases** page and run the packaged application.

Recommended for:
- test users,
- non-developer users,
- internal deployment,
- QA validation.

### Option 2. Run from source

#### Requirements
- Python 3.10+
- Windows 10/11 recommended

#### Core dependencies
```bash
pip install -r requirements.txt
```

#### Optional parser dependencies
```bash
pip install -r requirements-optional.txt
```

### Run
```bash
python main.py
```

### Smoke test
```bash
python smoke_check.py
```

## Build a Windows release

A typical PyInstaller-based build is used for Windows distribution.

Example:
```bash
python -m PyInstaller --clean --noconfirm --onedir --windowed --name DCoder_v4_8_260410 --paths . --add-data "resources;resources" --add-data "LICENSE;." --hidden-import pymavlink --hidden-import pyulog --hidden-import rosbags.highlevel --hidden-import mcap.reader --collect-submodules rosbags --collect-submodules mcap --collect-submodules matplotlib.backends --copy-metadata pyqtgraph --copy-metadata pandas --copy-metadata scipy --exclude-module PyQt5 --exclude-module PyQt6 --exclude-module PySide2 --exclude-module OpenGL --exclude-module pyqtgraph.opengl main.py
```

Before packaging, it is recommended to remove development leftovers such as:
- `__pycache__/`
- `*.pyc`
- old `build/` and `dist/`
- temporary sample outputs
- machine-specific session or settings files

## Project structure

```text
DCoder/
├─ api/
├─ application/
├─ backend/
│  ├─ analysis/
│  ├─ databank/
│  ├─ mapping/
│  ├─ parsers/
│  ├─ processing/
│  └─ sources/
├─ domain/
└─ frontend/
   └─ qt/
```

High-level design intent:
- **frontend**: Qt widgets, views, controllers
- **application**: use-case-oriented service layer
- **backend**: data parsing, processing, analysis, source adapters
- **domain**: contracts, models, app state

## Repository contents

Important files included in this repository:
- `main.py` — application entry point
- `requirements.txt` — core dependencies
- `requirements-optional.txt` — optional parsers and extended input support
- `USER_MANUAL.md` — end-user guide
- `ADMIN_MANUAL.md` — administrator / internal operator guide
- `LICENSE` — license terms

## Versioning and future updates

This repository is intended for continued version updates.

Recommended release practice:
- Use **GitHub Releases** for packaged builds
- Keep a clear release title such as `v4.8.0`, `v4.8.1`, `v4.9.0`
- Summarize each release with:
  - Added
  - Changed
  - Fixed
  - Known Issues

Suggested release asset naming:
- `DCoder_v4_8_0_win64.zip`
- `DCoder_v4_8_1_portable_win64.zip`

Suggested update policy:
- **Patch**: bug fixes, packaging fixes, UI defects
- **Minor**: new analysis functions, parser expansion, workflow improvements
- **Major**: structural redesign, data model changes, session compatibility changes

When a release changes session compatibility or file format behavior, mention it explicitly in the release note.

## Known limitations

Depending on the current release state, some advanced input paths may require optional packages or additional validation in the target environment.

Recommended before broad public distribution:
- test all target parser paths,
- validate session save/restore behavior,
- verify packaging on a clean Windows machine,
- confirm optional dependency handling.

## Security and operations note

DCoder supports developer-oriented extension paths such as add-on analysis functions.

If your deployment enables custom add-ons, treat them as executable Python code and manage them with the same care as internal scripts or plugins.

For production or company-wide use:
- review add-on sources,
- define a trusted add-on distribution policy,
- and separate public release assets from internal experimental extensions.

## Company and ownership

DCoder is developed by **[Company Name / Engineering Team]**.

Replace the placeholder above with your official organization name before public release.

Recommended company statement:
> Developed and maintained by [Company Name]. All product names, internal workflows, and packaged assets are managed by the company unless otherwise noted.

If your company uses a specific trademark, legal notice, support channel, or redistribution policy, add that information here.

## License

This project is distributed under the terms described in the `LICENSE` file included in this repository.

If your company plans to change the license before release, update both the `LICENSE` file and this section together.

## Support

For bug reports and feature requests:
- open a GitHub Issue,
- or contact **[support email / internal owner / team alias]**.

Recommended issue template categories:
- Bug report
- Feature request
- Parser/input issue
- Packaging issue
- UI/UX feedback

## Acknowledgements

DCoder reflects practical needs from real engineering workflows involving flight logs, time-series analysis, and experiment data inspection.

---

## Recommended README customization checklist before release

Replace the placeholders below before publishing:
- `[Company Name / Engineering Team]`
- `[support email / internal owner / team alias]`
- screenshots/GIFs
- final version number
- exact supported OS and Python versions
- final licensing statement if changed
