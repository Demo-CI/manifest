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
cd application
make build-deps-repo  # Uses ../libs/calculator
make
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
- Pinned to stable version tags (v1.0.0)

## GitHub Actions Integration

### Centralized Build System

The project uses a centralized build approach:

1. **Source repositories** (`application`, `static_library`) trigger builds via repository dispatch
2. **Build repository** contains the centralized workflow that:
   - Clones all required repositories
   - Builds static library and application
   - Runs tests and analysis
   - Collects artifacts

### Triggering Builds

Builds are automatically triggered when you push to:
- `application` repository → triggers centralized build
- `static_library` repository → triggers centralized build

The centralized build workflow handles:
- ✅ Cross-repository dependency management
- ✅ Static library compilation
- ✅ Application building and testing
- ✅ Artifact collection
- ✅ Build reporting

## Development Workflow

### Simple Development (Single Repository)
```bash
# Work on application only
git clone https://github.com/Demo-CI/application.git
cd application
make build-deps  # Fetches library dependency
make             # Build application
# Make changes, commit, push → triggers centralized build
```

### Multi-Repository Development (with Repo)
```bash
# Sync all repositories
repo sync

# Make changes across repositories
cd application
# Edit application code...
git add . && git commit -m "Update application"

cd ../libs/calculator  
# Edit library code...
git add . && git commit -m "Update library"

# Push changes
cd application && git push
cd ../libs/calculator && git push
# Each push triggers the centralized build system
```

## Build Commands Reference

### Application Build Commands
```bash
# Auto-detect build method (repo vs standalone)
make

# Build with external dependencies (standalone)
make build-deps

# Build with repo workspace dependencies
make build-deps-repo

# Run tests
make test

# Clean build artifacts
make clean
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

## Getting Started Examples

### Example 1: Simple Application Development
```bash
# Clone and build application
git clone https://github.com/Demo-CI/application.git
cd application
make  # Automatically fetches library and builds
./calculator  # Run the application
```

### Example 2: Multi-Repository Development
```bash
# Create workspace with all repositories
mkdir workspace && cd workspace
repo init -u https://github.com/Demo-CI/manifest.git
repo sync

# Build everything
cd application
make build-deps-repo  # Uses local ../libs/calculator
make
```

### Example 3: Library Development
```bash
# Work on the static library
git clone https://github.com/Demo-CI/static_library.git
cd static_library
make static  # Build the library
make test    # Test the library
```

## Project Goals

This project demonstrates:
- ✅ **Multi-repository management** using Google Repo tool
- ✅ **Centralized CI/CD** with GitHub Actions
- ✅ **Automated dependency management** between repositories
- ✅ **Cross-repository build coordination**
- ✅ **Simple C++ project structure** with external dependencies

Perfect for learning:
- Multi-repository workflows
- GitHub Actions automation
- C++ build system integration
- Dependency management strategies
