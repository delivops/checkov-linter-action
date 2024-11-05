# Checkov Application Manifests Linting Action

This GitHub Action runs Checkov linting on application manifests to validate custom policies and catch potential issues.

## Features

- Validates YAML files in the specified directory
- Checks custom Checkov policies from the `custom_policies` directory in this repo
- Optionally includes built-in Checkov checks
- Allows specifying which custom check IDs to run or skip
- Publishes Checkov results to the GitHub job summary
- Fails the workflow if any Checkov checks fail

## Usage

### Basic

```yaml
steps:
  - uses: delivops/checkov-linter-action@main
    with:
      directory: manifests/
```

This will run all custom Checkov checks on YAML files in the `manifests/` directory.

### Include built-in checks

```yaml
steps:
  - uses: delivops/checkov-linter-action@main
    with:
      directory: manifests/
      include_built_in_checks: true
```

Includes Checkov's built-in checks in addition to the custom checks.

### Specify check IDs to run

```yaml
steps:
  - uses: delivops/checkov-linter-action@main
    with:
      directory: manifests/
      check_ids: CKV2_CUSTOM_1,CKV2_CUSTOM_3
```

Only runs the custom checks with IDs `CKV2_CUSTOM_1` and `CKV2_CUSTOM_3`.

### Skip certain check IDs

```yaml
steps:
  - uses: delivops/checkov-linter-action@main
    with:
      directory: manifests/
      skip_check_ids: CKV2_CUSTOM_2
```

Skips running the custom check with ID `CKV2_CUSTOM_2`.

## Inputs

| Input                     | Description                                               | Required     | Default                  |
| ------------------------- | --------------------------------------------------------- | ------------ | ------------------------ |
| `directory`               | Directory to run Checkov in                               | <i>true</i>  |                          |
| `changed_files_only`      | Only check changed files (Default: `true` for PR context) | <i>false</i> | `false`                  |
| `checkov_output_folder`   | Output folder for Checkov results                         | <i>false</i> | `__results__`            |
| `check_ids`               | Comma-separated list of Checkov check IDs to run          | <i>false</i> | `""` (all custom checks) |
| `include_built_in_checks` | Include built-in checks in the scan                       | <i>false</i> | `false`                  |
| `skip_check_ids`          | Comma-separated list of Checkov check IDs to skip         | <i>false</i> | `""` (none skipped)      |
| `publish_to_job_summary`  | Publish Checkov results to GitHub job summary             | <i>false</i> | `false`                  |
| `debug`                   | Print debug information / Reports passed checks           | <i>false</i> | `false`                  |

## Outputs

- `summary`: Checkov results summary
