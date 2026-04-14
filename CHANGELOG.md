# Changelog

All notable changes to **springboot3** will be documented in this file.

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html) and the [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format.

---

## [2.0.0] - 2026-04-14

### Major Changes
- **Bumped to version 2.0.0** — Major internal refactoring while strictly preserving the ultra-defensive CIAO coding style.
- Completely overhauled the output system:
  - Introduced `output_text()` as the **single source of truth** for all human-readable text.
  - Introduced `output_json()` as the **single source of truth** for all machine-readable JSON output.
  - Full compliance with `--quiet` / `-q` and `--json` flags across the entire script.
- Strengthened root vs non-root installation isolation with new `get_install_bin_path()` helper.
- Added robust self-update safety:
  - Pure POSIX `version_gt()` function for semantic version comparison.
  - Prevents accidental downgrades when a newer development version is already installed.
  - Proper JSON support for `self-update` (including already-latest and newer-local cases).
- Improved interactive prompts with centralized `prompt_yes_no()` that fully respects `--quiet` and `--json`.
- Enhanced multi-user and harsh-environment support:
  - Better per-user storage isolation via `resolve_storage()`.
  - Early sourcing of user shell configuration (`source_user_shell_config()`) for reliable SDKMAN/Java/Maven availability in non-login shells.
- Added atomic file writing with `write_file_atomic()` to prevent partial or corrupted configuration files.
- Updated help and about commands with cleaner, more consistent output and full JSON support.
- Added explicit single-source-of-truth enforcement reminders in key functions to protect against future simplification by AI assistants or maintainers.
- Improved defensive coding throughout:
  - Repeated safe variable defaults in more functions.
  - Better respect for `--quiet`, `--json`, `--force`, `--reset`, `--project-dir`, and `--no-run` flags.
- Made `show_spring_boot_help()` reusable across the springboot family with smart major-version EOL warning detection (shows warning only for 2.x).

### Bug Fixes
- Fixed missing or malformed JSON output for `self-update` and `version-check`.
- Eliminated all raw `printf`/`echo`/`cat` outside the official output functions (full single-source-of-truth compliance).
- Corrected Alpine Linux instructions and SDKMAN setup messages to route through the output system.
- Fixed debug hints in `build_and_run()` to respect `--quiet` and `--json`.
- Removed copy-paste artifacts (old Spring Boot 2.7.18 references in headers and defaults).
- Fixed version warning logic in help text (now intelligently detects major version).

### Other Improvements
- Updated function headers with clearer GENERAL PURPOSE descriptions and explicit mentions of supported flags.
- Better documentation and warnings to guide future maintainers and AI assistants.
- Maintained full backward compatibility for the one-command install:  
  `curl -fsSL https://raw.githubusercontent.com/Wilgat/springboot3/main/springboot3 | bash`

### Notes
- Spring Boot **3.3.5** and Java **21 (Temurin)** remain **intentionally pinned**.
- This release focuses on reliability, maintainability, and robustness in harsh environments (containers, Alpine, Git Bash, multi-user systems, non-interactive shells) without sacrificing the project's defensive "verbose-on-purpose" philosophy.
- The help function is now shared/reusable with `springboot2` and `springboot4`.

---

## [1.6.0] - 2025 (Previous Stable)

- Initial mature version with solid CIAO defensive structure.
- Basic quiet/JSON support and installation logic.

---

## Unreleased

*(No changes yet)*

---

**GitHub**: https://github.com/Wilgat/springboot3

This changelog is maintained manually to ensure clarity and human readability.
