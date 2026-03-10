# springboot3

<img src="https://img.shields.io/badge/Version-1.0.12-blue?style=flat-square" alt="Version">  
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

## What it actually does (in order)

1. Installs **SDKMAN!** (if not already present)
2. Installs **Java 21** (Eclipse Temurin – current LTS)
3. Installs **Maven 3.9.9** (latest stable 3.9.x line)
4. Creates a fresh minimal project in `~/spring-boot-hello-springboot3`
   - Spring Boot **3.3.5** (latest in 3.3 line)
   - Single `@RestController` returning a text block greeting
   - Configured to bind to `0.0.0.0:8080`
5. Runs `mvn clean package`
6. Starts the application (`java -jar ...`)

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
# → springboot3 version1.0.13

springboot3 help
# shows this help
```

## Project location & cleanup

- Created in: `~/spring-boot-hello-springboot3`
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
- `--spring-boot-version=3.3.5` (when released)git 
- `--gradle` mode
- `--port=8080` / `--project-dir=/custom/path`
- `--no-run` / `--only-setup`
- Add actuator, security, or test dependencies optionally
- GitHub Actions for release tagging

## License

[MIT License](LICENSE)

Made with modern Java vibes and one coffee too many  
March 2026
