# actions-commitmsg-conform

A reusable GitHub Action workflow to enforce commit message best practices using [Conform](https://github.com/talos-systems/conform).

## Usage

### Basic Usage

```yaml
name: Validate Commit Message

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  validate-commit:
    uses: cloudbuildlab/actions-commitmsg-conform/.github/workflows/commitmsg-conform.yml@v1
```

### With Custom Configuration

```yaml
name: Validate Commit Message

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  validate-commit:
    uses: cloudbuildlab/actions-commitmsg-conform/.github/workflows/commitmsg-conform.yml@v1
    with:
      config: |
        policies:
          - type: commit
            spec:
              dco: false
              gpg:
                required: false
                gitHubOrganization: stacksmiths
              spellcheck:
                locale: US
              maximumOfOneCommit: false
              header:
                length: 89
                imperative: true
                case: lower
                invalidLastCharacters: .
              body:
                required: true
              conventional:
                types:
                  - chore
                  - ci
                  - docs
                  - feat
                  - fix
                  - refactor
                  - release
                  - revert
                  - style
                  - test
                scopes: [".*"]
```

## Versioning

This workflow follows semantic versioning. You can use it in two ways:

1. **Major Version Tag** (Recommended):

   ```yaml
   uses: cloudbuildlab/actions-commitmsg-conform/.github/workflows/commitmsg-conform.yml@v1
   ```

   This will automatically use the latest release within the v1.x.x series.

2. **Specific Version**:

   ```yaml
   uses: cloudbuildlab/actions-commitmsg-conform/.github/workflows/commitmsg-conform.yml@v1.0.1
   ```

   This pins to a specific version for maximum stability.

### Version History

See the [Releases](../../releases) page for a full list of versions and changes.

## Configuration

The workflow accepts a `config` input that allows you to provide a custom Conform configuration. If no configuration is provided, it will use the default configuration which enforces:

- Conventional commit types (chore, ci, docs, feat, fix, refactor, release, revert, style, test)
- Commit message length limits (89 characters)
- Imperative mood
- Lower case
- No trailing periods
- Required commit body
- Spell checking (US locale)
- Optional DCO and GPG signing

### Configuration Options

The configuration supports the following policies:

- `dco`: Enable/disable Developer Certificate of Origin
- `gpg`: GPG signing requirements
- `spellcheck`: Spell checking configuration
- `maximumOfOneCommit`: Limit to one commit
- `header`: Commit message header formatting
- `body`: Commit message body requirements
- `conventional`: Conventional commit type and scope rules

## Features

- Validates commit messages against configurable patterns
- Supports custom Conform configurations
- Easy to integrate into existing workflows
- Runs on pull request events by default
- Uses Docker for consistent execution
- GitHub reporter for detailed feedback

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
