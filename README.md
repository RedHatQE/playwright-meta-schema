# Playwright Metadata Validator

[![CI](https://github.com/RedHatQE/playwright-meta-schema/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/RedHatQE/playwright-meta-schema/actions/workflows/ci.yml)
[![Coverage Status](https://img.shields.io/codecov/c/github/RedHatQE/playwright-meta-schema/main.svg)](https://codecov.io/gh/RedHatQE/playwright-meta-schema)
[![Node.js Version](https://img.shields.io/node/v/playwright-meta-schema.svg)](https://nodejs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A TypeScript library that provides validation for Playwright test metadata including tags and annotations. This library helps ensure consistent and valid metadata across your Playwright test suite, with built-in support for JUnit reporting integration.

## Features

- ✅ **Tag Validation**: Validates Playwright test tags against predefined valid tags
- ✅ **Annotation Validation**: Validates test annotations with type-safe descriptions
- ✅ **TypeScript Support**: Full TypeScript support with comprehensive type definitions
- ✅ **CLI Tool**: Command-line interface for validation in CI/CD pipelines
- ✅ **Script Execution**: Integrate validation through yarn/npm scripts
- ✅ **Configurable**: Flexible configuration options for different environments
- ✅ **Comprehensive Testing**: Extensive test suite with 132+ tests

## Usage: CLI for CI/CD Pipelines

Use the CLI tool in your CI/CD linting pipelines to catch metadata validation errors early in the development process, before tests are executed.

The CLI tool provides fast, lightweight validation that integrates seamlessly with your existing linting and code quality checks.

```json
# Add to your CI/CD pipeline (package.json scripts)
{
  "scripts": {
    "validate:metadata": "playwright-meta-validator --fail-on-error",
    "lint": "eslint . && playwright-meta-validator --fail-on-error"
  }
}
```

## Installation

```bash
npm install playwright-meta-schema
# or
yarn add playwright-meta-schema
```

## Quick Start

Add metadata validation to your CI/CD pipeline:

```bash
# Install the package
npm install playwright-meta-schema
# or
yarn add playwright-meta-schema

# Add to package.json scripts
{
  "scripts": {
    "validate:metadata": "playwright-meta-validator --fail-on-error --verbose",
    "lint": "eslint . && playwright-meta-validator --fail-on-error"
  }
}

# Run in your CI pipeline
npm run validate:metadata
# or
yarn validate:metadata
```

## Valid Tags

### Playwright Built-in Tags

- `@skip` - Skip the test
- `@fail` - Mark test as expected to fail
- `@fixme` - Mark test as needing fixes
- `@slow` - Mark test as slow
- `@fast` - Mark test as fast

### Custom Tags

- `@smoke` - Smoke tests
- `@regression` - Regression tests
- `@sanity` - Sanity tests
- `@e2e` - End-to-end tests

## Valid Annotations

### Importance

```typescript
await test.info().annotate({ type: 'importance', description: 'critical' });
await test.info().annotate({ type: 'importance', description: 'high' });
await test.info().annotate({ type: 'importance', description: 'medium' });
await test.info().annotate({ type: 'importance', description: 'low' });
```

### Interface Type

```typescript
await test.info().annotate({ type: 'interface', description: 'ui' });
await test.info().annotate({ type: 'interface', description: 'api' });
await test.info().annotate({ type: 'interface', description: 'cli' });
await test.info().annotate({ type: 'interface', description: 'db' });
```

### Test Category

```typescript
await test.info().annotate({ type: 'category', description: 'unit' });
await test.info().annotate({ type: 'category', description: 'function' });
await test.info().annotate({ type: 'category', description: 'system' });
await test.info().annotate({ type: 'category', description: 'integration' });
await test.info().annotate({ type: 'category', description: 'performance' });
```

### Links and Assignees

```typescript
await test.info().annotate({
  type: 'link',
  description: 'https://jira.example.com/TICKET-123',
});
await test
  .info()
  .annotate({ type: 'assignee', description: 'john.doe@example.com' });
```

## CLI Usage

```bash
# Basic validation (demo mode - shows examples)
npx playwright-meta-validator

# Fail on validation errors (recommended for CI)
npx playwright-meta-validator --fail-on-error

# Verbose output for debugging
npx playwright-meta-validator --verbose --fail-on-error

# With custom configuration file
npx playwright-meta-validator --config ./metadata-config.json --fail-on-error
```

### CI/CD Integration Examples

```yaml
# GitHub Actions example
- name: Validate Playwright Metadata
  run: yarn validate:metadata

# GitLab CI example
lint:metadata:
  script:
    - yarn validate:metadata
```

### Package.json Script Integration

```json
{
  "scripts": {
    "validate:metadata": "playwright-meta-validator --fail-on-error",
    "lint": "eslint . && yarn validate:metadata",
    "ci": "yarn lint && yarn test"
  }
}
```

## Example: content-sources-frontend Integration

The content-sources-frontend project demonstrates how to integrate this validation tool:

```json
{
  "scripts": {
    "validate:metadata": "playwright-meta-validator --fail-on-error"
  }
}
```

This script can be run locally during development or as part of your CI/CD pipeline to ensure all test metadata is valid before tests execute.

## Development

```bash
# Install dependencies
yarn install

# Build the project
yarn build

# Run tests
yarn test

# Run tests with coverage
yarn test:coverage

# Lint and format code
yarn lint

# Test CLI functionality
yarn validate:playwright

# Run CLI with different options
npx playwright-meta-validator --verbose
npx playwright-meta-validator --fail-on-error
```

## Recommended Workflow

1. **Development**: Use CLI tool locally to validate metadata
   ```bash
   yarn validate:metadata
   ```

2. **CI/CD Pipeline**: Integrate CLI validation as a linting step
   ```bash
   yarn lint  # includes validate:metadata
   ```

3. **Pre-commit Hooks**: Optionally add validation to pre-commit hooks for early feedback

## Versioning

Semantic versioning will be used. Repository tags and GitHub release(s) will be provided.

## Releases

Releases will be done ad-hoc, automated and executed by CI, and will be triggered by repository tagging.

## Contributing

[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit)](https://github.com/pre-commit/pre-commit)
