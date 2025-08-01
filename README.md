# Demo-CI Project Manifest

[![Manifest Validation](https://github.com/Demo-CI/manifest/actions/workflows/validate.yml/badge.svg)](https://github.com/Demo-CI/manifest/actions/workflows/validate.yml)

Multi-repository C++ project demonstrating centralized CI/CD with GitHub Actions and Google Repo tool.

## 🚀 **Quick Start**

### Option 1: Multi-Repository Workspace (RECOMMENDED)
Use Google Repo tool for multi-repository development:

```bash
# Install repo tool
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.local/bin/repo
chmod +x ~/.local/bin/repo
export PATH="$HOME/.local/bin:$PATH"

# Setup workspace
mkdir demo-ci-workspace && cd demo-ci-workspace
repo init -u https://github.com/Demo-CI/manifest.git
repo sync

# Build everything
cd build
./scripts/build.sh build
./scripts/build.sh test
```

### Option 2: Individual Repository (Simple)
Work with individual repositories directly:

```bash
# Clone and build the application
git clone https://github.com/Demo-CI/application.git
cd application
make build-deps  # Automatically fetches static library
make             # Build application
make test        # Run tests
```

## 📋 **Available Manifests**

### `default.xml` (Main)
```bash
repo init -u https://github.com/Demo-CI/manifest.git
```
- All repositories from `main` branch
- Complete development environment

### `minimal.xml` (App Only)
```bash
repo init -u https://github.com/Demo-CI/manifest.git -m minimal.xml
```
- Application and static library only
- Faster setup for app development

### `development.xml` (Dev Branches)
```bash
repo init -u https://github.com/Demo-CI/manifest.git -m development.xml
```
- Uses `develop` branches for active development

### `production.xml` (Stable)
```bash
repo init -u https://github.com/Demo-CI/manifest.git -m production.xml
```
- Production-ready stable versions

## 🔧 **Repo Commands**

```bash
# Sync all repositories
repo sync

# Check status across all repos
repo status

# List all projects
repo list

# Run command in all repos
repo forall -c 'git status'
```

---

**🔗 Related:** [Centralized Build System](../build) | [Application](../application) | [Static Library](../static_library)
