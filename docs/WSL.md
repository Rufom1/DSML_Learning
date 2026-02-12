# WSL (Windows Subsystem for Linux) — Guide for this repo

This document explains how to set up WSL (recommended: WSL2) and integrate it with Visual Studio Code for development on Windows while maintaining portability to Unix deployments.

## Prerequisites

- Windows 10 (2004+) or Windows 11.
- Administrative privileges for initial setup.

## Install and enable WSL (quick)

Open an elevated PowerShell (Run as Administrator) and run:

```powershell
wsl --install
```

This installs WSL and a default Linux distro (typically Ubuntu). If you already have WSL but want WSL2 as the default, run:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
wsl --set-default-version 2
```

To list installed distros:

```powershell
wsl --list --verbose
```

## Initial distro setup

Open your distro (e.g., Ubuntu) from the Start menu or via `wsl` and update packages:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential curl git python3 python3-venv python3-pip
```

Create a project folder inside WSL (recommended path, e.g., `~/projects`):

```bash
mkdir -p ~/projects && cd ~/projects
# clone or move the repo here
```

Note: Storing and working on repository files inside the WSL filesystem (under `/home/<user>`) offers much better performance than editing files on the Windows drives (`/mnt/c/...`).

## Python & virtual environments

From the WSL shell in your project folder:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install -r requirements.txt   # if your project has dependencies
```

## VS Code integration

1. In Windows VS Code, install the `Remote - WSL` extension.
2. Open a new WSL window: press `Ctrl+Shift+P` and choose `Remote-WSL: New Window`.
3. From the WSL window, open the project folder (File → Open Folder) or run `code .` from the WSL shell to open VS Code in that context.

When VS Code is connected to WSL, extensions and terminals will run inside the Linux environment. Choose the interpreter from the WSL Python environment (the `.venv` you created).

## Docker and containers

For Docker integration, use Docker Desktop with WSL2 backend enabled. WSL-aware Docker runs natively inside WSL and allows `docker` commands from the WSL shell.

## Practical tips

- Access Windows files from WSL at `/mnt/c/...` but avoid editing large repos there.
- Keep your workspace in WSL for best performance.
- Update WSL kernel periodically: `wsl --update` (run in PowerShell).
- Restart all WSL instances: `wsl --shutdown`.

## Troubleshooting

- If VS Code cannot connect, confirm the `Remote - WSL` extension is installed and restart VS Code.
- Check distro status: `wsl --list --verbose`.
- If a command fails, check Windows Update and ensure Virtual Machine Platform is enabled.

## Useful commands

```powershell
# From Windows PowerShell (Admin)
wsl --install
wsl --set-default-version 2
wsl --list --verbose
wsl --shutdown
wsl --update
```

```bash
# From inside WSL
sudo apt update && sudo apt upgrade -y
python3 -m venv .venv
source .venv/bin/activate
code .   # opens VS Code from WSL
```

---

If you want, I can also add a short checklist or scripts to automate initial setup for contributors. Let me know if you'd like that.
