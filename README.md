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
- ✅ **CLI Tool**: **Recommended for CI/CD pipelines** - Command-line interface for validation
- ✅ **Runtime Validation**: Optional integration with Playwright's test.beforeEach hooks or auto fixtures
- ✅ **Configurable**: Flexible configuration options for different environments
- ✅ **Comprehensive Testing**: Extensive test suite with 132+ tests

## Recommended Usage: CLI for CI/CD Pipelines

**⚠️ STRONGLY RECOMMENDED**: Use the CLI tool in your CI/CD linting pipelines to catch metadata validation errors early in the development process, before tests are executed.

The CLI tool provides fast, lightweight validation that integrates seamlessly with your existing linting and code quality checks.

```json
# Add to your CI/CD pipeline (package.json scripts)
{
  "scripts": {
    "lint:metadata": "playwright-meta-validator --fail-on-error",
    "lint": "eslint . && playwright-meta-validator --fail-on-error"
  }
}
```

## Optional: Runtime Validation

**⚠️ CAUTION**: Runtime validation using beforeEach hooks or auto-fixtures should be considered **optional supplementary tools**. They add execution overhead to your test runs and should be used judiciously.

Runtime validation is best suited for:

- Development environments where immediate feedback is valuable
- Specific test suites where metadata validation is critical
- Debugging scenarios where detailed validation logging is needed

**Note**: Runtime validation will slow down your test execution as it runs validation logic before each test.

## Installation

```bash
npm install playwright-meta-schema
# or
yarn add playwright-meta-schema
```

## Quick Start

### CLI Validation (Recommended for CI/CD)

Add metadata validation to your CI/CD pipeline:

```bash
# Install the package
npm install playwright-meta-schema
# or
yarn add playwright-meta-schema

# Add to package.json scripts
{
  "scripts": {
    "lint:metadata": "playwright-meta-validator --fail-on-error --verbose",
    "ci:lint": "eslint . && playwright-meta-validator --fail-on-error"
  }
}

# Run in your CI pipeline
npm run lint:metadata
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

## CLI Usage (Recommended)

**Use the CLI tool in your CI/CD pipelines for optimal performance and early error detection.**

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
  run: npx playwright-meta-validator --fail-on-error

# Add to package.json for npm/yarn integration
{
  "scripts": {
    "lint": "eslint . && playwright-meta-validator --fail-on-error",
    "ci": "npm run lint && npm test"
  }
}
```

## Examples

See the `examples/` directory for:

- Basic usage examples
- Integration guide for content-sources-frontend
- Advanced configuration patterns

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
2. **CI/CD Pipeline**: Integrate CLI validation as a linting step
3. **Runtime Validation**: Optionally add for development environments only
4. **Performance**: Keep runtime validation minimal to avoid test execution overhead

## Versioning

Semantic versioning will be used. Repository tags and GitHub release(s) will be provided.

## Releases

Releases will be done ad-hoc, automated and executed by CI, and will be triggered by repository tagging.

## Contributing

[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit)](https://github.com/pre-commit/pre-commit)
