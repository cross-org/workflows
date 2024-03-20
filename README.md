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

1. **Reference the Workflow:** In your project's `.github/workflows` directory,
   create a new workflow file. Use the following syntax to reference a reusable
   workflow from this repository:

```yaml
uses: cross-org/workflows/<workflow-file>.yml@main
```

Replace `<workflow-file>` with the actual filename (e.g., `bun-ci.yml`).

### Integrating a part of a reusable workflow in your workflow

In your project's `.github/workflows/my-deno-workflow.yml`:

```yaml
name: My Project's Deno CI

on: 
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  deno_ci:
    uses: cross-org/workflows/deno-ci.yml@main
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
