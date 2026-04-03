Here's the **complete, polished `README.md`** for your **springboot3** project, written in the same style and structure as the updated `springboot2` README you approved earlier.

```markdown
# springboot3

<img src="https://img.shields.io/badge/Version-1.5.0-blue?style=flat-square" alt="Version">  
<img src="https://img.shields.io/badge/Java-21-orange?style=flat-square&logo=openjdk" alt="Java 21">  
<img src="https://img.shields.io/badge/Spring%20Boot-3.3.5-brightgreen?style=flat-square&logo=springboot" alt="Spring Boot 3.3.5">  
<img src="https://img.shields.io/badge/Maven-3.9.14-red?style=flat-square&logo=apachemaven" alt="Maven 3.9.14">  
<img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License">

**The friendliest way to run Spring Boot 3.3.5 in one command.**

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
- `--force` / `--reinstall`, `--quiet` support
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

## Program Structure (for curious people)

The script is intentionally kept **linear**, highly readable, and **extremely defensive** following the strict "ciao" coding style.

```text
┌─────────────────────────────────────────────────────────────┐
│  Header + Warnings + Project Constants                      │
│  (APP_NAME, VERSION, SCRIPT_URL, JAVA_ID, etc.)             │
├─────────────────────────────────────────────────────────────┤
│  Safe Variable Defaults (repeated on purpose)               │
│  Root Detection (IS_ROOT)                                   │
│  Force Flags & Quiet Mode                                   │
├─────────────────────────────────────────────────────────────┤
│  Color Output + Logging Functions (die, info, warn, etc.)   │
├─────────────────────────────────────────────────────────────┤
│  Core Utility Functions                                     │
│   • is_installed()            ← robust install detection    │
│   • get_installed_version()                                 │
│   • version_check()                                         │
│   • self_update()                                           │
│   • in_path() + add_to_shell_path()                         │
├─────────────────────────────────────────────────────────────┤
│  Installation Logic                                         │
│   • perform_self_install()    ← heart of self-install       │
│   • maybe_install()           ← interactive + auto-install  │
├─────────────────────────────────────────────────────────────┤
│  SDKMAN + Java + Maven Setup                                │
│   • check_alpine_requirements()                             │
│   • setup_sdkman()                                          │
│   • setup_java()                                            │
│   • setup_maven()                                           │
├─────────────────────────────────────────────────────────────┤
│  Project Management                                         │
│   • setup_springboot_project()                              │
│        ├── Preserves project by default                     │
│        └── Full reset with --force / --reinstall            │
├─────────────────────────────────────────────────────────────┤
│  Build & Run                                                │
│   • build_and_run()           ← ultra-defensive build + exec│
├─────────────────────────────────────────────────────────────┤
│  Help & Main Entry Point                                    │
│   • show_spring3_help()                                     │
│   • main()                                                  │
│        ├── Argument parsing                                 │
│        ├── Special handlers (--version, --self-update, etc.)│
│        ├── maybe_install() if needed                        │
│        └── Full setup flow                                  │
└─────────────────────────────────────────────────────────────┘
```

This structure makes the script easy to understand, copy, and adapt while protecting critical functions with heavy comments and warnings.

---

## Why the Heavy Defensive Style?

This project strictly follows the **ciao defensive coding style**:
- Repeated safe defaults (`: "${VAR:=default}"`)
- Redundant root / environment checks
- Heavy inline comments and `!!! DO NOT MODIFY OR SIMPLIFY !!!` blocks

**Purpose**:
- Survive harsh environments (`curl | bash`, non-interactive shells, missing `$HOME`, Alpine ash, Git Bash, etc.)
- Protect against accidental "cleaning" by AI assistants or contributors
- Serve as a reliable template for other defensive tools in the Wilgat family

---

## Project Philosophy

> "Write code that is easy to copy, hard to break, and self-documenting."

---

## Contributing

Please respect the strict defensive coding style and protective comments when submitting changes.

---

## License

MIT

---

**Part of the Wilgat defensive tool family.**  
*Last updated: April 2026*

---

**Note**: Spring Boot 3.3.5 is a current stable release (as of April 2026) with active community and commercial support. This tool provides a quick, reproducible way to spin up a minimal Spring Boot 3 + Java 21 application.
