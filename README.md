# .scripts

A lightweight, cross-platform environment configuration tool for macOS and Linux (Ubuntu/Debian). Automatically deploys a clean, high-performance shell environment based on Zsh and Oh My Zsh, fine-tuned for logging and Git status tracking.

### Key Features
* **Automated Bootstrapping** — Detects OS, updates package managers (Homebrew/APT), installs Zsh, and provisions required build/monitoring utilities.
* **Pro Terminal Styling** — Deploys custom `.prompt` and `.aliases` with non-blocking, responsive time logging right at the moment of execution.
* **Smart Enhancements** — Installs and updates `zsh-autosuggestions` and `zsh-syntax-highlighting` seamlessly.
* **Vim Sync** — Synchronizes `.vimrc` presets for optimized tabulations and text manipulation.

### Requirements
* **macOS** (Catalina or newer) or **Linux** (Ubuntu/Debian-based)
* Active internet connection for fetching dependencies
* `sudo` privileges for Linux system shell migration

## Installation

Run the following command in your terminal to download and execute the script interactively:

```bash
bash <(\curl -sSL https://raw.githubusercontent.com/Anobisoft/.scripts/main/.install) "$HOME/.scripts"
```
