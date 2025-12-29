# GitHub Actions Workflow Changes

## Summary

Created a new CI workflow for the opencode-vibe repository that uses the latest `actions/upload-artifact@v4` action.

## Changes Made

### 1. Created `.github/workflows/ci.yml`

A comprehensive CI workflow that includes:

- **Lint and Type Check Job**: Runs linting, type checking, and formatting validation
- **Test Job**: Runs all tests and uploads test coverage artifacts using `actions/upload-artifact@v4`
- **Build Job**: Builds the project and uploads build artifacts using `actions/upload-artifact@v4`

### 2. Upload Artifact Version: v3 → v4

The workflow uses `actions/upload-artifact@v4` instead of the deprecated `v3` version. This provides:

- Improved performance and reliability
- Better handling of large artifacts
- Enhanced error messaging
- Backward compatibility with v3 parameters

### 3. Key Features

- **Artifact Upload (Line 56)**: Uploads test coverage with `if-no-files-found: ignore` to gracefully handle cases where no coverage is generated
- **Artifact Upload (Line 82)**: Uploads build artifacts with:
  - Multi-line path specification for both dist and .next directories
  - Exclusion of `.next/cache` to reduce artifact size
  - 7-day retention period
  - Warning if no files are found

### 4. Bun Integration

The workflow is optimized for Bun (the project's package manager):
- Uses `oven-sh/setup-bun@v2` action
- Pins Bun version to 1.3.5 (matching package.json)
- Uses `--frozen-lockfile` for reproducible builds

## Migration Notes

The `actions/upload-artifact@v4` action is fully backward compatible with v3. The key parameters used:

- `name`: Artifact identifier
- `path`: Files/directories to upload (supports glob patterns and multi-line)
- `if-no-files-found`: Behavior when no files match (ignore/warn/error)
- `retention-days`: How long to keep artifacts (default is repository setting)

## Verification

To verify the workflow:

1. The workflow will run automatically on:
   - Pushes to `main` branch
   - Pull requests targeting `main` branch

2. You can manually check the workflow syntax at:
   - https://github.com/fglogan/opencode-vibe/actions

3. Artifacts will be available in the GitHub Actions UI after successful runs
