# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

Documentation-only repository for the **Comake Pi D3** development board (SigmaStar SCM8003G SoC, 8 TOPS IPU). It contains no source code, build system, or tests — do not look for build/lint/test commands here.

Two mirror documents plus their assets:

- `README.md` — Chinese quick-start guide (canonical)
- `README_EN.md` — English translation, mirrors `README.md` section-for-section
- `mymedia/` — flat directory of images referenced by both guides

## Conventions

- **Keep the two READMEs in sync.** Any content change must be made in both `README.md` and `README_EN.md`, preserving their section numbering.
- **Image naming**: bilingual screenshots use an `_en` suffix (e.g. `login.png` vs `login_en.png`); SVG diagrams (`board-main.svg`, `board-base.svg`, `sw-architecture.svg`) are language-neutral and shared.
- **Image references**: paths are relative to the repo root, e.g. `mymedia/board-main.svg`.

## Context not contained in this repo

The SDK source and build tooling are **not** checked in here; this repo only documents how to obtain and use them:

- SDK and tools are downloaded via `D3_debian_setup.sh` (Ubuntu desktop) or `D3_linux_setup.sh` (headless), cloned from `https://git.sigmastar.com.cn:9090/sigmastar/download_scripts.git`.
- The Git Web platform (`git.sigmastar.com.cn`) is **read-only** for external users — no personal repos or direct commits; feedback goes through the Comake community account and the issue tracker.
- Firmware is built via `bash D3_*_setup.sh build-image`, producing `SourceCode/project/image/output/images/UsbUpgradePackage/SgsUsbUpgrade.bin`.

Full download / build / flashing instructions live in the READMEs.
