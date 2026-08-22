# uvc - Conda-like Wrapper for uv

A lightweight wrapper for the `uv` Python package manager that mirrors conda's CLI commands for managing Python virtual environments.

## Overview

`uvc` (short for "uv conda") provides a simplified interface for managing Python virtual environments using the fast `uv` tool. It mimics the familiar conda command structure while leveraging the speed and efficiency of `uv`.

## Features

- **Conda-like Interface**: Familiar commands and flags (`create`, `remove`, `activate`)
- **Fast Environment Management**: Leverages `uv` for fast environment creation and management
- **Flexible Python Versioning**: Specify Python versions during environment creation
- **Package Management**: Install/uninstall packages within activated environments

## Installation

### Prerequisites

- `uv` must be installed on your system
- Bash- or Zsh-based shell (Linux/macOS/WSL)

### Install uvc

```bash
# Make sure uv is installed
brew install uv # macOS
curl -LsSf https://astral.sh/uv/install.sh | sh # Linux

# Download and install uvc
curl -sL https://raw.githubusercontent.com/audivir/uvc/main/uvc --output ~/.local/bin/uvc
chmod +x ~/.local/bin/uvc
```

## Usage

### Basic Commands

```bash
# Create a new environment
uvc create myenv

# Create environment with specific Python version
uvc create myenv -p 3.11

# Remove an environment (with confirmation)
uvc remove myenv

# Remove an environment without confirmation
uvc remove myenv --yes

# Activate an environment
uvc activate myenv

# List available environments
uvc envs
```

### Package Management Commands

```bash
# Install a package in the currently activated environment
uvc install ipykernel

# Uninstall a package from the currently activated environment
uvc uninstall ipykernel

# Install a .whl file that lives inside a git repo without cloning it.
uvc install-wheel org/repo wheels/pkg-1.0.0-py3-none-any.whl
uvc install-wheel git@github.com:org/repo.git wheels/pkg-1.0.0-py3-none-any.whl

# Run python within an environment (does not need to be activated)
uvc python myenv --version

# Run an arbitrary script within an environment (does not need to be activated)
uvc run myenv ipython --version
```

### Help

```bash
uvc --help
```

## Environment Storage

All environments are stored UVC_HOME or if it is not set in `~/.local/share/uvc`. This location follows the XDG Base Directory specification and keeps your environments organized.

## Activation Methods

There are two ways to activate environments with `uvc`:

### Method 1: Direct Evaluation (Temporary Activation)

```bash
eval "$(uvc activate myenv)"
```

This approach temporarily activates the environment in the current shell session. The activation is temporary and only affects the current shell session. It does not work any more if method 2 is used.

### Method 2: Shell Environment Setup (Permanent Activation)

```bash
# Add to your shell configuration file (~/.bashrc, ~/.zshrc, etc.)
uvc shellenv bash >> ~/.bashrc
uvc shellenv zsh >> ~/.zshrc

# Then reload your shell configuration
source ~/.bashrc

# Now you can activate environments directly
uvc activate myenv
```

This approach permanently sets up the shell environment so that `uvc activate` works directly without needing `eval`.

## Examples

### Create Environments

```bash
# Create environment with default Python
uvc create development

# Create environment with specific Python version
uvc create django-project -p 3.11

# Create environment with the latest Python version
uvc create web-app -p 3.12
```

### Manage Environments

```bash
# Remove environment with confirmation
uvc remove development

# Remove environment without confirmation
uvc remove development --yes

# List environments
uvc envs
```

### Activate Environments

```bash
# Activate environment (using eval method)
eval "$(uvc activate development)"

# Or, if you've set up shellenv (using direct method)
uvc activate development

# The activation is temporary and affects the current shell session
```

### Install/Uninstall Packages

```bash
# First, activate an environment
uvc activate development

# Then, install a package
uvc install requests

# Uninstall the package
uvc uninstall requests
```

## Requirements

- `uv` >= 0.1.0
- Bash or Zsh shell
- POSIX-compliant system (Linux/macOS)

## License

MIT License

## Contributing

Contributions are welcome! Please submit a pull request or open an issue for feature requests or bug fixes.

## Acknowledgments

- Built on top of the [`uv`](https://github.com/astral-sh/uv) Python package manager
- Inspired by the familiarity of conda's interface
