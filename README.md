# springboot3

<img src="https://img.shields.io/badge/Version-1.0.14-blue?style=flat-square" alt="Version">  
<img src="https://img.shields.io/badge/Java-21-orange?style=flat-square&logo=openjdk" alt="Java 21">  
<img src="https://img.shields.io/badge/Spring%20Boot-3.3.5-brightgreen?style=flat-square&logo=springboot" alt="Spring Boot 3.3">  
<img src="https://img.shields.io/badge/Maven-3.9.9-red?style=flat-square&logo=apachemaven" alt="Maven 3.9">  
<img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License">

**One stupidly simple command to get a modern Spring Boot 3.3 environment up and running in seconds.**

```bash
curl -fsSL https://raw.githubusercontent.com/Wilgat/springboot3/main/springboot3 | bash
```

→ installs SDKMAN! → Java 21 → Maven → creates a minimal Hello World project → builds it → runs it on port 8080

Perfect when you need to:

- quickly spin up a clean Spring Boot 3.x playground
- verify compatibility / behavior on Java 21 (or prepare for Java 25)
- demonstrate current Spring Boot + modern Java setup
- onboard someone to Spring Boot 3 without fighting tool versions

## Requirement Analysis

This section explains the major design decisions behind the `springboot3` installer script.

- **Shell choice** — `#!/bin/bash`  
  The script depends heavily on **SDKMAN!**, whose official install & init logic uses bash-isms and is documented/tested primarily in bash. POSIX `sh` would be fragile/unreliable here.

- **User privileges** — auto-detect root vs normal user  
  - root → installs to `/usr/local/bin`  
  - normal user → installs to `~/.local/bin` (creates dir if needed)

- **Self-install support** — yes, classic `curl | bash` friendly  
  Hard-codes script name (`springboot3`) instead of using `$0` (which breaks under `curl | bash`).

- **Temporary files** — safe atomic install (`mktemp` → write → `mv`)

- **PATH handling** — for normal users:  
  idempotently appends `~/.local/bin` to `~/.bashrc` if missing  
  shows clear "run `. ~/.bashrc`" message

- **Installation check** — smart: normal users check both global **and** user-local path

- **Other constraints**  
  - Clear progress messages at every step  
  - Small, named functions → easier to read/modify  
  - No `set -euo pipefail` (prefer explicit checks)  
  - Keeps bash because SDKMAN init requires it

## Pseudo-code Overview

High-level flow of what the script does (in execution order):

| Step | Section / Function              | What it does                                                                 |
|------|----------------------------------|------------------------------------------------------------------------------|
| 1    | Header & constants               | Defines version, colors, URLs, Java/Maven/Spring versions, paths             |
| 2    | Install location logic           | Detects root vs user → sets `INSTALL_DIR` & `INSTALL_PATH`                   |
| 3    | Helpers (`is_installed`, `in_path`, etc.) | Checks if already installed, if dir in `$PATH`, etc.                   |
| 4    | Self-install (`perform_self_install`) | If missing: downloads to temp → chmod → atomic mv → adds to PATH if needed |
| 5    | `maybe_self_install`             | Runs self-install only if needed (non-interactive friendly)                  |
| 6    | Argument parsing                 | Handles `help`, `version`, default = run                                     |
| 7    | `setup_sdkman`                   | Installs SDKMAN! if missing → sources init → verifies `sdk` works            |
| 8    | `setup_java`                     | `sdk install java 21-temurin` → sets default                                 |
| 9    | `setup_maven`                    | `sdk install maven 3.9.9` → sets default                                     |
| 10   | `setup_spring_project`           | Deletes old project → creates `pom.xml` + `HelloApplication.java` + properties |
| 11   | `build_and_run`                  | `mvn clean package` → `java -jar` (prefers SDKMAN java)                      |
| 12   | `main`                           | Parse args → maybe install self → show header → run all setup steps          |

## What it actually does (in order)

1. Installs **itself** (if missing) to `~/.local/bin` or `/usr/local/bin`
2. Installs **SDKMAN!** (if not already present)
3. Installs **Java 21** (Eclipse Temurin – current LTS)
4. Installs **Maven 3.9.9** (latest stable 3.9.x line)
5. Creates a fresh minimal project in `~/springboot-hello-springboot3`
   - Spring Boot **3.3.5** (latest in 3.3 line)
   - Single `@RestController` returning a text block greeting
   - Configured to bind to `0.0.0.0:8080`
6. Runs `mvn clean package`
7. Starts the application (`java -jar ...`)

After ~1–3 minutes (depending on internet & machine) you should see:

```
Tomcat started on port(s): 8080 (http) ...
```

Open http://localhost:8080 (or your machine's IP from another device)

## Installation

**Recommended way** (always use `bash` explicitly):

```bash
curl -fsSL https://raw.githubusercontent.com/Wilgat/springboot3/main/springboot3 | bash
```

If you need root privileges (e.g. writing to `/usr/local/bin`):

```bash
sudo curl -fsSL https://raw.githubusercontent.com/Wilgat/springboot3/main/springboot3 | sudo bash
```

**Do NOT use `sh`** — the script relies on bash features (especially for SDKMAN compatibility).

### Smart install behavior

- **Root / sudo** → installs to `/usr/local/bin/springboot3`
- **Normal user** → installs to `~/.local/bin/springboot3`
  - creates the directory if missing
  - adds `export PATH="$HOME/.local/bin:$PATH"` to `~/.bashrc` if needed
  - shows instruction to run `. ~/.bashrc` or open new terminal

Interactive terminals ask for confirmation.  
Piped/non-interactive runs install automatically.

## Usage

```bash
springboot3
# → setup everything → create project → build → run on :8080

springboot3 version
# → springboot3 version 1.0.14

springboot3 help
# shows this help
```

## Project location & cleanup

- Created in: `~/springboot-hello-springboot3`
- Re-running `springboot3` → **deletes old folder** and recreates fresh
- Want to keep experiments? → rename/move the folder before re-running

## Requirements

- `bash` (not pure `sh` / dash / ash)
- `curl`
- internet connection (first run)
- ~600–1200 MB disk space (SDKMAN caches + Java + Maven)

No Docker, no manual `JAVA_HOME`, no fighting with toolchains.

## Why this exists

Spring Boot 3.x (started in late 2022) brought baseline Java 17, virtual threads (Java 21+), GraalVM native support, observability improvements, and many modern defaults.

This tiny script removes 90% of the "but on my machine it's Java 8…" friction when you want a **genuine Spring Boot 3 + Java 21** environment in seconds.

## Contributing

Ideas welcome:

- `--java=25` / `--java=21-tem` / `--java=latest`
- `--spring-boot-version=3.3.5` (when released)
- `--gradle` mode
- `--port=8080` / `--project-dir=/custom/path`
- `--no-run` / `--only-setup`
- Add actuator, security, or test dependencies optionally
- GitHub Actions for release tagging

## License

[MIT License](LICENSE)

Made with modern Java vibes and one coffee too many  
March 2026
