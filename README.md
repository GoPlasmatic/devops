# Plasmatic DevOps

Centralized GitHub Action workflows for releasing Rust crates across GoPlasmatic repositories.

## Overview

This repository maintains reusable CI/CD workflows for automated release processes, ensuring consistent quality checks and deployment procedures across all Plasmatic Rust projects.

## Repository Structure

```
.github/workflows/
├── rust-library-release.yml      # Base template
├── swiftmtmessage-release.yml    # SwiftMTMessage library
├── mxmessage-release.yml         # MXMessage library
├── dataflow-rs-release.yml       # dataflow-rs library
├── datalogic-rs-release.yml      # datalogic-rs library
├── datafake-rs-release.yml       # datafake-rs library
└── reframe-release.yml           # Reframe application
```

## Workflows

### Libraries (Published to crates.io)
- **SwiftMTMessage** - SWIFT MT message parsing
- **MXMessage** - MX message handling  
- **dataflow-rs** - Data flow processing
- **datalogic-rs** - Data logic implementation
- **datafake-rs** - Fake data generation

### Applications
- **Reframe** - Binary application releases

## Features

✅ Automated code quality checks (fmt, clippy, tests)  
✅ Version conflict detection  
✅ Automatic git tagging  
✅ GitHub release creation  
✅ crates.io publishing  
✅ Dry run mode for testing  

## Quick Start

### Option 1: Copy to Target Repository
1. Copy the appropriate workflow file from `.github/workflows/` to target repo's `.github/workflows/`
2. Ensure `CRATES_IO_TOKEN` org secret is available
3. Update version in `Cargo.toml`
4. Trigger workflow manually from Actions tab

### Option 2: Trigger from This Repository
1. Navigate to the Actions tab in this repository
2. Select the appropriate workflow for your library/application
3. Click "Run workflow"
4. The workflow will checkout the target repository and perform the release

## Requirements

- Rust stable toolchain
- GitHub organization secrets:
  - `CRATES_IO_TOKEN` - For publishing to crates.io
  - `GH_PAT` - Personal Access Token with repo permissions for pushing tags

## License

Apache License 2.0