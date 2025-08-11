# Plasmatic DevOps

Centralized GitHub Action workflows for releasing Rust crates across GoPlasmatic repositories.

## Overview

This repository provides a reusable workflow system for automated releases, ensuring consistent quality checks and deployment procedures across all Plasmatic Rust projects.

## Architecture

```
.github/workflows/
├── rust-release-reusable.yml     # Core reusable workflow (all logic here)
├── release-*.yml                 # Simple triggers for each repository
└── triggers/
    └── release-all.yml           # Bulk release multiple projects

templates/
├── library-release-caller.yml    # Template for library repos
└── application-release-caller.yml # Template for application repos
```

## Usage Options

### Option 1: Trigger from This Repository
Navigate to Actions tab → Select workflow → Run workflow

Available workflows:
- `Release SwiftMTMessage`
- `Release MXMessage`
- `Release dataflow-rs`
- `Release datalogic-rs`
- `Release datafake-rs`
- `Release Reframe`
- `Release Multiple Projects` (bulk releases)

### Option 2: Add Workflow to Target Repository
Copy the appropriate template to target repo's `.github/workflows/release.yml`:
- Libraries: Use `templates/library-release-caller.yml`
- Applications: Use `templates/application-release-caller.yml`

### Option 3: Direct Reusable Workflow Call
```yaml
jobs:
  release:
    uses: GoPlasmatic/devops/.github/workflows/rust-release-reusable.yml@main
    with:
      repository: GoPlasmatic/your-repo
      package-type: library  # or application
      dry-run: false
    secrets:
      GH_PAT: ${{ secrets.GH_PAT }}
      CRATES_IO_TOKEN: ${{ secrets.CRATES_IO_TOKEN }}
```

## Features

✅ **Automated Quality Checks**
- Code formatting (`cargo fmt`)
- Linting (`cargo clippy`)
- Test execution (`cargo test`)

✅ **Smart Package Detection**
- Handles both single packages and workspaces
- Automatically selects publishable packages
- Supports binary and library detection

✅ **Release Management**
- Version conflict detection
- Automatic git tagging
- GitHub release creation
- crates.io publishing (libraries)
- Binary packaging (applications)

✅ **Safety Features**
- Dry run mode for testing
- Duplicate version prevention
- Cross-repository operation support

## Required Secrets

Configure as organization-level secrets:

- **`CRATES_IO_TOKEN`** - For publishing to crates.io
- **`GH_PAT`** - Personal Access Token with `repo` scope
  - Required for pushing tags and creating releases
  - Create at: Settings → Developer settings → Personal access tokens

## Monitored Projects

### Libraries
- **SwiftMTMessage** - SWIFT MT message parsing
- **MXMessage** - MX message handling
- **dataflow-rs** - Data flow processing
- **datalogic-rs** - Data logic implementation
- **datafake-rs** - Fake data generation

### Applications
- **Reframe** - Binary application

## Workflow Details

The reusable workflow (`rust-release-reusable.yml`) handles:

1. **Repository checkout** with PAT authentication
2. **Rust toolchain setup** with latest stable
3. **Dependency caching** for faster builds
4. **Code quality checks** (format, lint, test)
5. **Package detection** (workspace-aware)
6. **Version validation** against crates.io
7. **Git tag creation** and pushing
8. **GitHub release** with documentation
9. **Publishing** to crates.io or binary packaging
10. **Status reporting** with clear output

## License

Apache License 2.0