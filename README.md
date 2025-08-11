# Plasmatic DevOps

Centralized GitHub Action workflows for releasing Rust crates across GoPlasmatic repositories.

## Overview

This repository maintains reusable CI/CD workflows for automated release processes, ensuring consistent quality checks and deployment procedures across all Plasmatic Rust projects.

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

1. Copy workflow to target repo's `.github/workflows/`
2. Ensure `CRATES_IO_TOKEN` org secret is available
3. Update version in `Cargo.toml`
4. Trigger workflow manually from Actions tab

## Requirements

- Rust stable toolchain
- GitHub organization secrets:
  - `CRATES_IO_TOKEN` (for crates.io publishing)

## License

Apache License 2.0