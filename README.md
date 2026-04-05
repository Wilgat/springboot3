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

## Contributing

Please respect the strict defensive coding style and protective comments when submitting changes.

---

## License

MIT
