# Anobisoft Terminal Environment

![Shell](https://img.shields.io/badge/shell-zsh%20%7C%20bash-4acc13?style=flat-square&logo=gnu-bash&logoColor=white)
![OS Compatible](https://img.shields.io/badge/os-macOS%20%7C%20Linux-000000?style=flat-square&logo=apple&logoColor=white)
![Font](https://img.shields.io/badge/font-JetBrains%20Mono%20NF-blueviolet?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-orange?style=flat-square)

An automated environment provisioning and synchronization system built on top of **Zsh** and **GNU** core utilities. Fully compatible with **macOS** and major **Linux** distributions (Debian/Ubuntu, Fedora, Arch).

> 🌐 **Русская версия:** Документация на русском языке доступна в файле [README.ru.md](README.ru.md).

## Key Features

*   **GNU Toolchain on macOS:** Automatically replaces native BSD utilities (`sed`, `awk`, `grep`, `find`, etc.) with their modern GNU equivalents without forcing the `g` prefix.
*   **Reactive Prompt Engine (`.prompt`):** Real-time clock and Git status updates (every second) driven by native Zsh hooks without terminal lag.
*   **Stream Isolation (`.functions`):** The `hlstderr` wrapper intercepts `STDERR`, strips internal file/line prefixes, and prints errors in bright red.
*   **Network Profiling (`.curl_templates`):** Pre-configured JSON headers and performance timing templates for `cURL` (DNS lookup, connect, transfer start, total time).
*   **macOS System Optimization (`config_macOS`):** Enforces ISO format for Xcode logs, trims trailing whitespace on save, and blocks `.DS_Store` generation on network/USB shares.
*   **Style Enforcement (`.editorconfig`):** Universal formatting rules (Unix `LF` line endings, 4 spaces for indentation) with native support in Xcode 16+ and VS Code.

## Repository Structure

```text
├── .install            # Main interactive installer script (hidden to prevent accidental execution)
├── .anobirc            # Core runcom file (automatically sourced in ~/.zshrc)
├── .alias              # System shortcuts and Xcode cache cleaning tools
├── .functions          # Custom shell functions for advanced stream manipulation
├── .prompt             # Dynamic reactive prompt engine configuration
├── .curl_templates     # Network profiling aliases and cURL headers
├── .vimrc              # Minimalistic Vim configuration file
├── .editorconfig       # Global IDE code style guidelines
└── once/
    ├── config_macOS    # macOS and Xcode defaults tuning script
    └── config_git      # Global Git configurations script
```

## Quick Start (Installation)

The installer script is hidden by design to prevent accidental overwrites. To deploy the environment directly from GitHub, run the following command in your terminal:

```bash
bash <(\curl -sSL https://raw.githubusercontent.com/Anobisoft/.scripts/main/.install) "\$HOME/.scripts"
```

### Custom Installation Path
You can change the target directory by modifying the path argument at the end of the command:
```bash
bash <(\curl -sSL https://raw.githubusercontent.com/Anobisoft/.scripts/main/.install) "/var/custom/path"
```

Once the setup is complete, reload your shell configuration:
```bash
source ~/.zshrc
```

## Core Components Usage

### 1. Error Highlighting with `hlstderr`
Wrap any binary or long-running script into `hlstderr` to isolate and highlight errors:
```bash
hlstderr cat /nonexistent/file
```

### 2. API Profiling with `curlog` / `curlapi`
Executes requests with an explicit breakdown of network performance stages:
```bash
# Basic JSON API request with timing telemetry
curlog https://example.com

# Authenticated request with dynamic \$HEADER_TOKEN evaluations
export HEADER_TOKEN="Bearer your_token_here"
curlapi https://example.com
```

### 3. Xcode Maintenance with `xclear` / `killxcode`
*   `xclear` — Sequentially and safely wipes `DerivedData`, Clang `ModuleCache`, and Xcode general caches. Uses strict fail-safe chains to halt execution if a step fails.
*   `killxcode` — Raw PID extraction and forceful termination (`SIGKILL -9`) of stuck Xcode processes and zombie simulator servers.

## VS Code Integration

To get proper syntax highlighting for extensionless scripts (`.anobirc`, `.prompt`, etc.) and enforce `.editorconfig` rules, add these associations to your project `.vscode/settings.json`:

```json
{
    "files.associations": {
        ".install": "shellscript",
        ".functions": "shellscript",
        ".anobirc": "shellscript",
        ".prompt": "shellscript",
        ".alias": "shellscript",
        ".curl_templates": "shellscript"
    },
    "[shellscript]": {
        "editor.fontFamily": "'JetBrainsMono Nerd Font', 'JetBrains Mono', monospace",
        "editor.fontLigatures": true,
        "editor.fontSize": 13
    }
}
```
*(Requires the **EditorConfig for VS Code** extension to handle formatting rules properly).*
