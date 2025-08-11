# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the Plasmatic DevOps repository that maintains GitHub Action workflows for releasing Rust crates across multiple GoPlasmatic repositories. The primary purpose is to provide consistent, automated release processes for all maintained libraries and applications.

## Repository Structure

```
devops/
├── .github/
│   └── workflows/
│       ├── rust-library-release.yml      # Base template for Rust library releases
│       ├── swiftmtmessage-release.yml    # SwiftMTMessage library workflow
│       ├── mxmessage-release.yml         # MXMessage library workflow
│       ├── dataflow-rs-release.yml       # dataflow-rs library workflow
│       ├── datalogic-rs-release.yml      # datalogic-rs library workflow
│       ├── datafake-rs-release.yml       # datafake-rs library workflow
│       └── reframe-release.yml           # Reframe application workflow
├── CLAUDE.md
└── README.md
```

## Workflow Features

All workflows are manually triggered (workflow_dispatch) and include:

1. **Code Quality Checks**:
   - `cargo fmt` - Enforces code formatting standards
   - `cargo clippy` - Runs linting with warnings as errors
   - `cargo test` - Runs all tests with all features enabled

2. **Version Management**:
   - Reads version from Cargo.toml
   - Verifies version doesn't already exist on crates.io
   - Creates git tags automatically

3. **Release Process**:
   - Creates GitHub releases with proper documentation
   - Publishes to crates.io (libraries only)
   - Packages binaries for applications

4. **Safety Features**:
   - Dry run option to test workflow without publishing
   - Version conflict detection
   - Automatic tag management

## Required Secrets

These secrets must be configured in the target repositories:

- `GITHUB_TOKEN` - For git operations and release creation (auto-provided by GitHub)
- `CRATES_IO_TOKEN` - Organization-level secret for publishing to crates.io (required for library releases)

## Usage Instructions

### Deploying Workflows

1. Copy the appropriate workflow file to the target repository's `.github/workflows/` directory
2. Configure required secrets in the repository settings
3. Trigger manually from the Actions tab with optional dry run

### Running a Release

1. Ensure version is updated in Cargo.toml
2. Go to Actions tab in the repository
3. Select the release workflow
4. Click "Run workflow"
5. Optional: Enable dry_run for testing

### Workflow Customization

When modifying workflows:
- Test with dry_run enabled first
- Ensure all quality checks pass before release
- Update release notes template as needed
- Consider adding platform-specific builds for applications

## Monitored Repositories

1. **SwiftMTMessage** - SWIFT MT message parsing library
2. **MXMessage** - MX message handling library  
3. **dataflow-rs** - Data flow processing library
4. **datalogic-rs** - Data logic implementation library
5. **datafake-rs** - Fake data generation library
6. **Reframe** - Application (not published to crates.io)

## Development Guidelines

- All workflows use Ubuntu latest for consistency
- Rust stable toolchain is used for all builds
- Caching is implemented for faster builds
- Version bumping is handled in repository commits, not in workflows
- Tags follow semantic versioning with 'v' prefix (e.g., v1.2.3)