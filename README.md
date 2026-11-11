# dotfiles

A personal, terminal-centric development environment for Linux and macOS.

A curated collection of shell configurations, terminal tools, themes and productivity scripts, designed to provide a consistent workflow across machines.

## Features

- **Zsh** — Shell configuration, aliases, functions and shared history.

- **Starship** — Context-aware shell prompt.

- **Kitty** — GPU-accelerated terminal emulator.

- **Tmux** — Terminal multiplexer with custom status line and plugins.

- **FZF** — Fuzzy finder with theme-aware colors.

- **Git** — Global configuration and worktree-based development workflow.

- **Tmuxinator** — Manage persistent terminal sessions.

- **Themes** — Unified color palettes across the terminal environment.

- **System metrics** — CPU load, memory, GPU and network monitoring.

- **Custom scripts** — Small utilities for everyday terminal workflows.

- **Dotbot** — Declarative symlink management.

## Installation

### Requirements

- Git

- Bash

- curl

- sudo privileges on Linux

- A supported package manager:

  - APT

  - DNF

  - Pacman

  - Homebrew

### Quick start

Clone the repository and run the bootstrap script:

```bash

git clone https://github.com/rabelius/dotfiles.git

cd dotfiles

./install.sh

```

The installer is designed to be idempotent and detects macOS/Linux and the available package manager.

### Install flow

The setup follows five stages:

1. **Bootstrap** — `install.sh` detects the operating system and package manager, installs dependencies and prepares the environment.

2. **Submodules** — `git submodule sync` and `git submodule update --init --recursive` initialize the required submodules.

3. **Dotbot** — Applies `install.conf.yaml` and creates the symbolic links for the shell, terminal, Tmux, Starship, FZF, themes and custom scripts.

4. **Tmux plugins** — TPM installs `tmux-sensible` and `tmux-yank`.

5. **Validation** — `test/validate.sh` checks that the expected symbolic links exist and resolve correctly.

The bootstrap script handles dependency installation, submodule initialization and Dotbot configuration. TPM plugin installation and validation are separate steps unless explicitly invoked by the installer.

### What gets installed

The bootstrap script installs the required command-line tools and supporting applications, including:

- Zsh

- Tmux

- FZF

- Git

- FD

- Ripgrep

- Bat

- Htop

- Tealdeer

- Tmuxinator

- Kitty

- Tree

- Binutils

- Cheat

- Starship

- Oh My Zsh

Package availability varies between operating systems and package managers.

## Themes as data

A single variable controls the visual identity of the entire terminal environment:

```bash

DOTFILES_THEME="mint"

```

Change the value to switch between available palettes.

### Available themes

| Theme | Palette |

|---|---|

| `lavender` | Catppuccin Mocha |

| `rose` | Rosé Pine |

| `mint` | Everforest |

| `peach` | Kanagawa Wave |

| `gentle` | Terminal defaults |

### Shared theme contract

Each theme exposes a consistent set of `THEME_*` variables consumed by the configuration and helper scripts.

Examples:

- `THEME_FZF_COLORS`

- `THEME_EMOJI_SESSION_POINTER`

Theme definitions drive the appearance of:

- Kitty color schemes

- Starship prompt

- Tmux status line

- FZF interface

- Shell prompt glyphs (`❯`, `◈`, `✦`)

The goal is to define colors and visual behavior once and reuse them consistently across the environment.

## Tmux status & system metrics

The Tmux status line provides system and network information, refreshed every 5 seconds.

| Component | Information |

|---|---|

| `tmux-metrics` | System load, memory usage and GPU utilization |

| `tmux-net-stat` | Network upload and download rates |

GPU utilization is collected through `nvidia-smi` when an NVIDIA GPU and its drivers are available.

## Shell environment

The shell configuration focuses on productivity, consistency and an uninterrupted command-line workflow.

### History

- 100,000 history entries.

- Shared history across terminal panes and sessions.

- Immediate history writes.

### Interactive commands

The following commands are configured to request confirmation before potentially destructive operations:

- `rm`

- `cp`

- `mv`

### Command-line tools

The environment integrates FZF, FD, Ripgrep, Bat, Tealdeer and other utilities to improve searching, navigation and everyday terminal operations.

## Git worktree workflow

Repositories follow a consistent directory structure:

```text

~/gt/<repo>/crew/<branch>

```

Each Git worktree gets its own Tmux window.

This makes it possible to work on multiple branches simultaneously, keeping independent working directories and terminal sessions without constantly switching branches or stashing changes.

## Configuration management

Dotbot manages the configuration through symbolic links.

The mapping between repository files and their destinations is defined in:

```text

install.conf.yaml

```

The linked configuration includes:

| Source | Destination |

|---|---|

| Zsh configuration | `~/.zshrc` |

| Tmux configuration | `~/.tmux.conf` |

| FZF configuration | `~/.fzf.zsh` |

| Starship configuration | `~/.config/starship.toml` |

| Kitty configuration | `~/.config/kitty/kitty.conf` |

| Tmuxinator | `~/.config/tmuxinator` |

| Themes | `~/.config/dotfiles/themes` |

| Custom scripts | `~/.local/bin` |

Configuration files remain in the repository; symbolic links expose them at their expected locations.

Pulling new changes updates the linked files on the machine.

## Repository structure

```text

dotfiles/

├── bin/                  # Custom executables

├── dotbot/               # Dotbot submodule

├── fzf/                  # FZF configuration

├── git/                  # Git configuration

├── kitty/                # Kitty terminal configuration

├── scripts/              # Custom utility scripts

├── starship/             # Starship prompt configuration

├── test/                 # Validation scripts

├── themes/               # Shared color palettes

├── tmux/                 # Tmux configuration and plugins

├── tmuxinator/           # Tmuxinator sessions

├── zsh/                  # Zsh configuration

├── install               # Dotbot entry point

├── install.conf.yaml     # Dotbot configuration

└── install.sh            # Bootstrap installer

```

## Updating

Pull the latest changes and synchronize submodules:

```bash

cd ~/dotfiles

git pull --recurse-submodules

git submodule update --init --recursive

```

Because configuration files are symlinked, changes to tracked files become available immediately.

Re-run the installer when package dependencies or system-level configuration need updating:

```bash

./install.sh

```

## Safety notes

The installer makes system-level changes and should be reviewed before execution.

- Package installation may require `sudo`.

- Existing configuration files covered by the backup routine are moved to `~/.dotfiles.bak/`.

- The default shell is changed to Zsh.

- Kitty may be configured as the default GNOME terminal.

- Some packages, such as `texlive-full`, can require substantial disk space.

Review `install.sh` and `install.conf.yaml` before installing, especially when adapting the configuration to an existing environment.

---

**Maintained by [@rabelius](https://github.com/rabelius)**

[Repository](https://github.com/rabelius/dotfiles)
