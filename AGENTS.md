# Repository Guidelines

## Project Structure & Module Organization
Godot is a large C++ engine organized by subsystem. Core runtime code lives in `core/`, startup flow in `main/`, gameplay/framework layers in `scene/` and `servers/`, platform backends in `platform/`, rendering/audio/input backends in `drivers/`, optional features in `modules/`, and editor code in `editor/`. Third-party vendored code is in `thirdparty/` (avoid editing unless required). Tests are in `tests/` (mirrors engine areas), docs tooling/content in `doc/`, and maintenance scripts in `misc/`.

## Build, Test, and Development Commands
- `scons platform=linuxbsd target=editor dev_build=yes` builds a local development editor.
- `scons platform=linuxbsd target=editor dev_build=yes tests=yes` builds with unit tests enabled.
- `./bin/godot.linuxbsd.editor.dev.x86_64 --headless --test --force-colors` runs unit tests (binary name varies by platform/arch).
- `pre-commit run -a` runs configured format/lint/documentation checks.
- `pre-commit run --hook-stage manual clang-tidy` runs `clang-tidy` (requires up-to-date `compile_commands.json`).

## Coding Style & Naming Conventions
Follow `.editorconfig`, `.clang-format`, and `.clang-tidy`.
- Indentation: tabs (size 4) for most files; Python, `SConstruct`, and `SCsub` use spaces.
- Line length: 120.
- Python lint/format: `ruff` (plus `mypy` typing checks).
- C/C++ formatting: `clang-format`.
- Test file naming: `tests/<area>/test_<snake_case>.cpp` (see `tests/create_test.py`).

## Testing Guidelines
Add tests for bug fixes and new behavior in the same PR whenever possible. Prefer regression-style tests that fail before the fix and pass after it. Keep tests close to the affected area (`tests/core`, `tests/scene`, etc.).

## Commit & Pull Request Guidelines
Use focused commits and PRs (one topic per PR). Commit titles should be imperative, capitalized, and typically under 72 chars (e.g., `Fix crash when reloading imported scene`). Optional subsystem prefixes are common (e.g., `Core:`). Target `master`, rebase instead of merge from upstream, and link issues in PR descriptions (e.g., `Fixes #1234`). For behavior/UI changes, include clear reproduction steps and screenshots when helpful.

## Agent-Specific Note
If contributing via an autonomous AI agent, follow `CONTRIBUTING.md` disclosure requirements (PR title prefix and description disclosure).
