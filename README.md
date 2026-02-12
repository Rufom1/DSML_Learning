# DSML_Learning
Repo environment for Data Science and Machine Learning Topics

## Using WSL for Windows development

This repository is typically used on Windows. For a Unix-like development environment and better parity with Linux deployments, use Windows Subsystem for Linux (WSL).

- **Why WSL:** provides a lightweight Linux kernel and environment on Windows for better compatibility with Linux tooling, Docker, and CI/CD workflows.
- **Recommendation:** keep your project files inside the WSL filesystem (e.g., under your distro's home directory) for best I/O performance.

### Quickstart (high level)

1. Enable WSL and install a distro (WSL2 recommended).
2. Install developer packages in the distro (Python, Git, build tools).
3. Install the VS Code "Remote - WSL" extension and open the project from WSL.

For a step-by-step guide and VS Code integration details see: [docs/WSL.md](docs/WSL.md)
