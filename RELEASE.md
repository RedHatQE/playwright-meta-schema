# Release Process

This document describes how to release a new version of `playwright-meta-schema` to npm.

## Overview

The release process is fully automated through GitHub Actions. The version is determined by the Git tag created during the release, **not** by the version in `package.json`. This means you don't need to make any commits to update the version number.

## Prerequisites

- You must have admin/maintainer access to the repository
- The `NPM_TOKEN` secret must be configured in the repository settings
- All changes you want to release must be merged to the `main` branch

## Release Steps

### 1. Navigate to GitHub Releases

Go to: https://github.com/RedHatQE/playwright-meta-schema/releases

### 2. Create a New Release

1. Click **"Draft a new release"**
2. Click **"Choose a tag"**
3. Type the new version tag in the format `vX.Y.Z` (e.g., `v1.0.0`, `v1.2.3`, `v2.0.0-beta.1`)
   - The tag **must** start with `v`
   - Use semantic versioning: `MAJOR.MINOR.PATCH`
   - For pre-releases, add a suffix like `-alpha.1`, `-beta.2`, `-rc.1`
4. Select **"Create new tag: vX.Y.Z on publish"** from the dropdown
5. Set the target to `main` branch
6. Enter a release title (e.g., `Release 1.0.0` or `v1.0.0`)
7. Add release notes describing:
   - New features
   - Bug fixes
   - Breaking changes
   - Any other relevant information
8. If this is a pre-release (alpha, beta, rc), check the **"Set as a pre-release"** checkbox
9. Click **"Publish release"**

### 3. Automated Publishing

Once you publish the release:

1. GitHub Actions will automatically trigger the workflow
2. The workflow will:
   - Run linting and tests
   - Build the package
   - Extract the version from your tag (e.g., `v1.0.0` → `1.0.0`)
   - Update `package.json` with the correct version
   - Publish to npm with provenance
   - Update the GitHub release with npm installation instructions

### 4. Verify Publication

After a few minutes:

1. Check the [Actions tab](https://github.com/RedHatQE/playwright-meta-schema/actions) to ensure the workflow succeeded
2. Verify the package on npm: https://www.npmjs.com/package/playwright-meta-schema
3. The GitHub release will be automatically updated with npm installation instructions

## Version Numbering

Follow [Semantic Versioning](https://semver.org/):

- **MAJOR** version (X.0.0): Breaking changes
- **MINOR** version (0.X.0): New features, backwards compatible
- **PATCH** version (0.0.X): Bug fixes, backwards compatible

### Examples

- `v1.0.0` - First stable release
- `v1.1.0` - New feature added
- `v1.1.1` - Bug fix
- `v2.0.0` - Breaking changes
- `v2.0.0-beta.1` - Beta pre-release
- `v2.0.0-rc.1` - Release candidate

## Troubleshooting

### Workflow doesn't trigger

- Ensure you created a **release**, not just a tag
- Verify the tag starts with `v`
- Check that the target is the `main` branch

### Workflow fails

1. Check the [Actions tab](https://github.com/RedHatQE/playwright-meta-schema/actions) for error details
2. Common issues:
   - Tests failing: Fix the tests and create a new release
   - NPM_TOKEN expired: Update the secret in repository settings
   - Build errors: Ensure the code builds locally first

### Wrong version published

If you accidentally publish the wrong version:

1. Deprecate the wrong version on npm: `npm deprecate playwright-meta-schema@X.Y.Z "Wrong version, use X.Y.Z instead"`
2. Create a new release with the correct version tag

## Important Notes

- **Never manually edit `package.json` version**: The version is automatically set from the Git tag
- The `package.json` version field is kept at `0.0.0` in the repository - this is intentional
- Always create releases from the `main` branch
- Tag names must start with `v` followed by the version number
- You cannot re-publish the same version - if you need to fix something, increment the version
