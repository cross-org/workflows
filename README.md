# Cross-Org Reusable Workflows

This repository provides a collection of reusable GitHub Actions workflows
designed to streamline CI/CD practices across your (but primarily our) projects.

## Available Workflows

- **`.github/workflows/deno-ci.yml`:** Installs latest version of Deno, checks
  formatting, linting, lints docs, and runs tests.
- **`.github/workflows/bun-ci.yml`:** Installs latest version of Bun, installs
  JSR dependencies, runs tests.
- **`.github/workflows/node-ci.yml`:** Installs oldes LTS and latest version of
  Node.js, installs JSR dependencies, runs tests.
- **`.github/workflows/jsr-publish.yml`:** Automates publishing to JSR.

## How to Use

In your project's `.github/workflows/testing-ci.yml`:

```yaml
name: Testing CI

on: 
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:  # Allow manual runs

jobs:
  deno_ci:
    uses: cross-org/workflows/.github/workflows/deno-ci.yml@main
    with:
      entrypoint: mod.ts
  bun_ci:
    uses: cross-org/workflows/.github/workflows/bun-ci.yml@main
    with:
      jsr_dependencies: "@cross/test @std/assert"
  node_ci:
    uses: cross-org/workflows/.github/workflows/node-ci.yml@main
    with:
      jsr_dependencies: "@cross/test @std/assert"
      test_target: "*.test.ts" # Optional
```

In your project's `.github/workflows/jsr-publish.yml`:

```yaml
name: Publish to jsr.io
on:
  release:
    types: [released]
  workflow_dispatch:

jobs:
  publish:
    permissions:
      contents: read
      id-token: write
    uses: cross-org/workflows/.github/workflows/jsr-publish.yml@main
```

2. **Customize (Optional):** Reusable workflows can accept inputs to tailor
   their behavior. Refer to the individual workflow files for available
   parameters.

## Contributing

We welcome contributions! To propose a new workflow or improvements to existing
ones:

1. **Fork the repository.**
2. **Create your feature branch.**
3. **Submit a pull request with a detailed description of changes.**

## License

This repository's contents are released under the MIT License:
[https://choosealicense.com/licenses/mit/](https://choosealicense.com/licenses/mit/).
