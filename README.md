# Demo-CI Project Manifest

[![Manifest Validation](https://github.com/Demo-CI/manifest/actions/workflows/validate.yml/badge.svg)](https://github.com/Demo-CI/manifest/actions/workflows/validate.yml)

Simple multi-repository project for exploring GitHub Actions capabilities with C++ calculator application and static library.

## Project Overview

This is a demonstration project that showcases:
- ✅ Multi-repository management with Google Repo
- ✅ Centralized build system using GitHub Actions
- ✅ C++ application with external library dependency
- ✅ Automated CI/CD workflows

## Repository Structure

| Repository | Path | Description |
|------------|------|-------------|
| **application** | `application/` | Main C++ calculator application |
| **static_library** | `libs/calculator/` | Calculator math utilities library |
| **build** | `build/` | Centralized build system and workflows |
| **toolchain** | `toolchain/` | Development tools and utilities |

## Quick Start

### Option 1: Individual Repository Development (Recommended)
For simple development, you can work with individual repositories:

```bash
# Clone and build the application
git clone https://github.com/Demo-CI/application.git
cd application
make build-deps  # Automatically fetches static library
make             # Build application
make test        # Run tests
```

### Option 2: Multi-Repository Workspace with Repo Tool

Install Google's `repo` tool:
```bash
# Download and install repo tool
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.local/bin/repo
chmod +x ~/.local/bin/repo
export PATH="$HOME/.local/bin:$PATH"
```

Create workspace:
```bash
# Create and initialize workspace
mkdir demo-ci-workspace && cd demo-ci-workspace
repo init -u https://github.com/Demo-CI/manifest.git
repo sync

# Build the project
# Navigate to build directory
cd build
./run.sh build all           # Clean → Build → Test → Analyze → Docs
```

### Workspace Structure (with repo tool)

```
demo-ci-workspace/
├── .repo/                 # Repo metadata
├── application/           # Main calculator application
├── libs/calculator/       # Static library (from static_library repo)
├── build/                 # Build system and CI/CD scripts
└── toolchain/             # Development tools
```

## Available Manifests

### `default.xml` - Standard Development
```bash
repo init -u https://github.com/Demo-CI/manifest.git
```
- All repositories from `main` branch
- Includes all components: application, library, build system, and toolchain

### `minimal.xml` - Application Development Only
```bash
repo init -u https://github.com/Demo-CI/manifest.git -m minimal.xml
```
- Only application and static library
- Faster setup for application developers

### `development.xml` - Development Branch
```bash
repo init -u https://github.com/Demo-CI/manifest.git -m development.xml
```
- Uses `develop` branches for active development

### `production.xml` - Stable Release
```bash
repo init -u https://github.com/Demo-CI/manifest.git -m production.xml
```

### Useful Repo Commands (if using multi-repo workspace)
```bash
# Sync all repositories
repo sync

# Check status of all repositories
repo status

# Show current manifest
repo manifest

# List all projects
repo list

# Execute command across all repos
repo forall -c 'git status'
```
