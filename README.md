# Lint Kit Analyze GitHub Action

A GitHub Action that runs Dart static analysis using [Lint Kit](https://pub.dev/packages/lint_kit) - a powerful toolkit for creating custom Dart lints and quick actions.

## About Lint Kit

Lint Kit is a comprehensive static analysis framework that extends Dart's built-in analyzer capabilities. It allows you to:

- **Define custom lints** with configurable severity levels (hint, info, warning, error)
- **Create code actions** for quick fixes and refactoring suggestions
- **Build project-specific conventions** and automated checks
- **Share reusable analyzers** across teams and projects
- **Debug lints interactively** with full IDE integration

Unlike traditional linting tools, Lint Kit works **alongside** the Dart analyzer to provide enhanced, project-specific analysis capabilities.

## Usage

Add this action to your workflow to automatically analyze your Dart code with Lint Kit:

```yaml
name: Static Analysis
on: [push, pull_request]

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: your-org/lint_kit_analyze@v1
        with:
          fatal-warnings: true
          paths-to-analyze: "lib test"
```

## Inputs

| Input                     | Description                                   | Required | Default |
| ------------------------- | --------------------------------------------- | -------- | ------- |
| `fatal-warnings`          | Treat warnings as errors, failing the CI      | No       | `false` |
| `fatal-infos`             | Treat info messages as errors, failing the CI | No       | `false` |
| `workspace-root`          | Root directory of the workspace to analyze    | No       | `.`     |
| `paths-to-analyze`        | Specific files or directories to analyze      | No       | `.`     |
| `verbose`                 | Enable verbose logging output                 | No       | `false` |
| `package-logs`            | Always package and upload logs as artifacts   | No       | `false` |
| `package-logs-on-failure` | Package logs only when analysis fails         | No       | `false` |

## Examples

### Basic Analysis

```yaml
- uses: your-org/lint_kit_analyze@v1
```

### Strict Analysis (Warnings as Errors)

```yaml
- uses: your-org/lint_kit_analyze@v1
  with:
    fatal-warnings: true
    fatal-infos: true
```

### Analyze Specific Directories

```yaml
- uses: your-org/lint_kit_analyze@v1
  with:
    paths-to-analyze: "lib packages/core"
    verbose: true
```

### With Log Collection

```yaml
- uses: your-org/lint_kit_analyze@v1
  with:
    package-logs-on-failure: true
    verbose: true
```

## What This Action Does

1. **Sets up the environment**: Installs Dart and activates the Lint Kit CLI
2. **Manages caching**: Efficiently caches Lint Kit data between runs
3. **Starts services**: Launches the Lint Kit LSP server and analyzer
4. **Runs analysis**: Executes static analysis on your specified paths
5. **Handles results**: Reports findings and optionally packages logs
6. **Saves cache**: Preserves cache for faster subsequent runs

## Requirements

- Your repository must contain a Dart project with a `pubspec.yaml`
- A Lint Kit configuration should be present (created via the Dart Lint Kit VSCode extension or manually)

## Getting Started with Lint Kit

If you haven't set up Lint Kit in your project yet:

1. Install the [Dart Lint Kit VSCode extension](https://marketplace.visualstudio.com/items?itemName=DartLintKit.dart-lint-kit)
2. Run `Dart Lint Kit: Create Lint Kit Package` from the command palette
3. Customize your lints in the generated package
4. Add this GitHub Action to your workflow

## Related

- [Lint Kit Package](https://pub.dev/packages/lint_kit) - Core package for defining custom lints
- [Lint Kit CLI](https://pub.dev/packages/lint_kit_cli) - Command-line interface
- [VSCode Extension](https://marketplace.visualstudio.com/items?itemName=DartLintKit.dart-lint-kit) - IDE integration
