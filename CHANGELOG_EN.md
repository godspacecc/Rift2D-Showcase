# Rift2D Changelog

All notable changes to this project will be documented in this file.

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

[English](CHANGELOG_EN.md) | [中文](CHANGELOG.md)

---

## [Unreleased]

### Added
- Nothing yet

### Changed
- Nothing yet

### Fixed
- Nothing yet

---

## [0.1.0] - 2026-06-25

First release, core systems foundation complete.

### Added
- **Architecture**: Unity 2022.3 + QFramework-style layers (Model/System/Command/Controller/Event)
- **Scene Flow**: Boot → Lobby → Dungeon → Return to lobby, complete game loop skeleton
- **Save System**: Multi-slot saves, create/load/continue/delete
- **Inventory**: Prototype inventory system with basic structure
- **Resource Pipeline**: YooAsset loading pipeline, local/remote resources support
- **Configuration**: Luban XML/CSV workflow
- **Hot Update**: HybridCLR integration, Boot (host) and Game (hot update) assembly separation
- **Multiplayer**: Minimal realtime multiplayer validation, TCP protocol, local/LAN testing
- **Toolchain**:
  - UI generation tool
  - Asset reference diagnostics
  - Animation diagnostics
  - YooAsset packaging helper
  - Localization helper
  - Server deployment helper
- **Testing**: Unity EditMode tests, .NET server tests, headless TCP smoke tests
- **Showcase Repo**: GitHub Actions auto-sync docs and releases to showcase repo

### Changed
- Nothing

### Fixed
- Nothing

[Unreleased]: https://github.com/godspacecc/Rift2D-Showcase/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/godspacecc/Rift2D-Showcase/releases/tag/v0.1.0