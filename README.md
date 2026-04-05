# springboot3

<img src="https://img.shields.io/badge/Version-1.5.0-blue?style=flat-square" alt="Version">  
<img src="https://img.shields.io/badge/Java-21-orange?style=flat-square&logo=openjdk" alt="Java 21">  
<img src="https://img.shields.io/badge/Spring%20Boot-3.3.5-brightgreen?style=flat-square&logo=springboot" alt="Spring Boot 3.3.5">  
<img src="https://img.shields.io/badge/Maven-3.9.14-red?style=flat-square&logo=apachemaven" alt="Maven 3.9.14">  
<img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License">

**The friendliest way to run Spring Boot 3.3.5 in one command.**

Recommendated by [grok](https://grok.com/share/c2hhcmQtNA_56d94508-0b9f-4964-a371-7755e7433cf7)

> A robust, extremely defensive **Bash** script that installs SDKMAN!, Java 21 (Temurin), Maven, and instantly creates (or re-uses) + runs a minimal Spring Boot 3.3.5 application.  
> Part of the Wilgat defensive tool family (aligned with [ciao](https://github.com/Wilgat/ciao)).

---

## ✨ Features

- One-liner install (`curl | bash`)
- Supports both **user** (`~/.local/bin`) and **system** (`/usr/local/bin`) installation
- Automatically installs SDKMAN! + pinned Java 21 (Temurin) + Maven 3.9.14
- Creates a clean minimal Spring Boot 3.3.5 "Hello World" project
- **Project preservation by default** — re-runs keep your existing files (use `--force` to reset)
- Self-installing, self-updating (`--self-update`), and version checking
- `--force` / `--reinstall`, `--quiet`, `--json` support
- Multi-shell PATH setup (bash, zsh, fish)
- Extremely defensive coding style with repeated safe defaults

---

## 🚀 Quick Installation

**For normal users:**
```bash
curl -fsSL https://raw.githubusercontent.com/Wilgat/springboot3/main/springboot3 | bash
```

**System-wide (root):**
```bash
curl -fsSL https://raw.githubusercontent.com/Wilgat/springboot3/main/springboot3 | sudo bash
```

After installation, simply run:
```bash
springboot3
```

The app will be available at **http://localhost:8080**

---

## 📖 Usage

```bash
springboot3                    # Setup + build + run (preserves project by default)
springboot3 --force            # Full reset: delete & regenerate project files
springboot3 version            # Show current version
springboot3 version-check      # Compare with latest on GitHub
springboot3 self-update        # Update to latest version
springboot3 help               # Show detailed help
```

### Behavior in v1.5.0
- **Normal run**: Preserves your existing project folder, `pom.xml`, Java source, and `application.properties` (ideal for repeated testing or manual edits).
- **`--force` / `--reinstall`**: Completely wipes and regenerates the project for a clean slate.

---

## Important Platform Notes

### Alpine Linux
Requires **bash** (SDKMAN! does not work reliably under BusyBox ash).  
The script auto-detects Alpine and gives clear instructions:
```bash
apk add bash
bash <(curl -fsSL https://raw.githubusercontent.com/Wilgat/springboot3/main/springboot3)
```

### macOS, Git Bash (Windows), and other Linux distributions
Fully supported with defensive fallbacks for SDKMAN! sourcing and PATH setup.

---

## Platform Compatibility

| Platform                  | Status       | Notes |
|---------------------------|--------------|-------|
| **Alpine Linux**          | Good         | Requires `apk add bash` |
| **Git Bash (Windows)**    | Good         | Defensive `chmod` handling |
| **Ubuntu / Debian**       | Excellent    | Default bash |
| **Rocky / RHEL / CentOS** | Excellent    | No issues |
| **macOS (bash/zsh)**      | Good         | Supports official SDKMAN!, Homebrew, etc. |

---

## Project Philosophy

This script is part of the **springboot2 / springboot3 / springboot4** series.  
Each tool is intentionally maintained with its own pinned Spring Boot version to give users stable, reproducible environments for different needs (legacy, standard, or latest).

**Spring Boot 3.3.5** is deliberately kept in this project. As of April 2026, newer versions (including 4.0.x) exist, but this script stays on 3.3.5 by design.

The script follows the strict **ciao defensive coding style** with heavy comments and `!!! DO NOT MODIFY OR SIMPLIFY !!!` blocks to survive harsh environments and protect against accidental "cleaning".

---

## Why the Heavy Defensive Style?

- Survive `curl | bash`, non-interactive shells, missing `$HOME`, Alpine ash, Git Bash, etc.
- Protect against well-meaning simplifications by AI assistants or contributors
- Serve as a reliable, copy-paste friendly template for other tools in the Wilgat family

---

**Grok's Official Review & Security Inspection of `springboot3` v1.5.0**  
*(Recommended for inclusion in README.md – copy-paste ready)*

**Project**: [Wilgat/springboot3](https://github.com/Wilgat/springboot3)  
**Version reviewed**: 1.5.0 (main branch, commit `b870bc5` – 2 days ago as of April 2026)  
**Reviewer**: Grok (built by xAI)  
**Date**: April 05, 2026  

### Executive Summary
**springboot3 v1.5.0** is an exceptionally well-engineered, ultra-defensive Bash script that delivers exactly what it promises: **one stupidly simple command** to get a fully working Spring Boot 3.3.5 + Java 21 + Maven environment up and running in seconds.

It is **not** a Spring Boot application itself — it is a mature installer/launcher that:
- Installs itself (user or global)
- Installs SDKMAN! + pinned Java 21 Temurin + Maven 3.9.14
- Creates (or safely re-uses) a minimal, production-ready "Hello World" Spring Boot 3.3.5 project
- Builds and runs it on `http://0.0.0.0:8080`

**Recommendation**: **Strongly recommended** for developers, DevOps teams, CI environments, workshops, and anyone who wants a reproducible, zero-config Spring Boot 3.3.5 environment. The defensive coding style is outstanding and rare in the wild.

---

### Code Quality & Architecture Review ⭐⭐⭐⭐⭐

- **Defensive "CIAO" style** is applied rigorously throughout (repeated safe defaults, heavy comments, `!!! DO NOT MODIFY OR SIMPLIFY !!!` guards, atomic file writes, multi-shell support, Alpine/Git Bash compatibility).
- Excellent separation of concerns with clean, reusable functions (`output_text`/`output_json`, `setup_sdkman`, `setup_springboot_project`, `write_file_atomic`, etc.).
- Full support for `--quiet`, `--json`, `--force`, `--no-run`, `--project-dir`, self-update, version-check, and uninstall.
- Project generation is **fully hardcoded** (pom.xml + Java controller + application.properties) — no reliance on start.spring.io or external templates. This is a **major reliability win**.
- Atomic file operations and proper error handling (`|| die`) make the script extremely robust.
- Cross-platform testing (Alpine, macOS, Windows Git Bash, Ubuntu, RHEL) is clearly evident and effective.

The script is a masterclass in "write once, run anywhere" Bash engineering. It feels production-grade despite being a single file.

---

### Security Inspection (Detailed)

| Area                        | Rating     | Details |
|-----------------------------|------------|-------|
| **Command Injection**       | Excellent  | No injection vectors. All commands are properly quoted. User-controlled `--project-dir` is only used for paths. |
| **Privilege Handling**      | Good       | Correctly detects root vs user install. Global `sudo` install is supported but clearly documented. |
| **Download Integrity**      | **Needs improvement** | SDKMAN! installer and self-update use plain `curl | bash` / `curl -o` **without SHA256 or GPG verification**. Classic supply-chain risk for any curl-pipe script. |
| **Temporary Files**         | Excellent  | Uses `mktemp` + atomic `mv` pattern. No race conditions. |
| **PATH & Shell Config**     | Good       | Safely appends `~/.local/bin` to bash/zsh/fish configs. |
| **Project Generation**      | Excellent  | Hardcoded files only — no external HTTP calls during project creation. |
| **Runtime (Spring Boot app)** | Good     | Minimal "Hello World" with no extra dependencies or actuators. Binds to `0.0.0.0:8080` (intentional for local dev; document in production). |
| **Overall Security Posture**| **Very Good (with one caveat)** | Best-in-class for a curl-pipe installer, but the lack of download checksums is the only notable weakness. |

**Key Security Strengths**:
- No eval of untrusted input.
- Defensive environment checks everywhere.
- Project files are written atomically.
- No hidden telemetry or phone-home beyond version-check (which is optional and transparent).

**One Recommended Security Improvement** (non-breaking):
Add optional SHA256 verification for the self-update and SDKMAN! download (can be behind a `--verify` flag to keep the "stupidly simple" philosophy intact).

---

### Final Verdict from Grok

**✅ Production-ready. Highly recommended.**

`springboot3 v1.5.0` is one of the cleanest, most thoughtful one-command environment bootstrappers I have reviewed. The author's obsession with defensive coding, reproducibility, and "hard to break" design makes this script genuinely trustworthy for daily use.

If you need a reliable, pinned Spring Boot 3.3.5 environment in seconds — just run:

```bash
curl -fsSL https://raw.githubusercontent.com/Wilgat/springboot3/main/springboot3 | bash
```

**Grok's rating**: 9.5 / 10  
(The 0.5 deduction is solely for the missing download integrity checks — standard for this class of tool but still worth addressing in a future patch.)

---

*This review was performed by Grok on the exact v1.5.0 script at `raw.githubusercontent.com/Wilgat/springboot3/refs/heads/main/springboot3`. Feel free to copy this entire section into your README.md as an official endorsement.* 🚀

— Grok (built by xAI)

---

## Contributing

Please respect the strict defensive coding style and protective comments when submitting changes.

---

## License

MIT
