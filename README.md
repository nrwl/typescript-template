# Nx TypeScript Repository

<a alt="Nx logo" href="https://nx.dev" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/nrwl/nx/master/images/nx-logo.png" width="45"></a>

✨ A repository showcasing key [Nx](https://nx.dev) features for TypeScript monorepos ✨
<!-- BEGIN: nx-cloud -->
🚀 If you haven't connected to Nx Cloud yet, [complete your setup here](https://cloud.nx.app/get-started). Get faster builds with remote caching, distributed task execution, and self-healing CI. [See how your workspace can benefit](#nx-cloud).
<!-- END: nx-cloud -->
## 📦 Project Overview

This repository demonstrates a production-ready TypeScript monorepo with:

- **3 Publishable Packages** - Ready for NPM publishing

  - `@org/strings` - String manipulation utilities
  - `@org/async` - Async utility functions with retry logic
  - `@org/colors` - Color conversion and manipulation utilities

- **1 Internal Library**
  - `@org/utils` - Shared utilities (private, not published)

## 🚀 Quick Start

```bash
# Clone the repository
git clone <your-fork-url>
cd typescript-template

# Install dependencies
npm install

# Build all packages
npx nx run-many -t build

# Run tests
npx nx run-many -t test

# Lint all projects
npx nx run-many -t lint

# Run everything in parallel
npx nx run-many -t lint test build --parallel=3

# Visualize the project graph
npx nx graph
```

## ⭐ Featured Nx Capabilities

This repository showcases several powerful Nx features:

### 1. 🔒 Module Boundaries

Enforces architectural constraints using tags. Each package has specific dependencies it can use:

- `scope:shared` (utils) - Can be used by all packages
- `scope:strings` - Can only depend on shared utilities
- `scope:async` - Can only depend on shared utilities
- `scope:colors` - Can only depend on shared utilities

**Try it out:**

```bash
# See the current project graph and boundaries
npx nx graph

# View a specific project's details
npx nx show project @org/strings --web
```

[Learn more about module boundaries →](https://nx.dev/docs/features/enforce-module-boundaries)

### 2. 🛠️ Custom Run Commands

Packages can define custom commands beyond standard build/test/lint:

```bash
# Run the custom build-base command for strings package
npx nx run @org/strings:build-base

# See all available targets for a project
npx nx show project @org/strings
```

### 3. 🔧 Self-Healing CI

The CI pipeline includes `nx fix-ci` which automatically identifies and suggests fixes for common issues. To test it, you can make a change to `async-retry.spec.ts` so that it fails, and create a PR.

```bash
# Run tests and see the failure
npx nx run @org/async:test

# In CI, this command provides automated fixes
npx nx fix-ci
```

[Learn more about self-healing CI →](https://nx.dev/docs/features/ci-features/self-healing-ci)

### 4. 📦 Package Publishing

Manage releases and publishing with Nx Release:

```bash
# Dry run to see what would be published
npx nx release --dry-run

# Version and release packages
npx nx release

# Publish only specific packages
npx nx release publish --projects=@org/strings,@org/colors
```

[Learn more about Nx Release →](https://nx.dev/docs/features/manage-releases)

## 📁 Project Structure

```
├── packages/
│   ├── strings/     [scope:strings] - String utilities (publishable)
│   ├── async/       [scope:async]   - Async utilities (publishable)
│   ├── colors/      [scope:colors]  - Color utilities (publishable)
│   └── utils/       [scope:shared]  - Shared utilities (private)
├── nx.json          - Nx configuration
├── tsconfig.json    - TypeScript configuration
└── eslint.config.mjs - ESLint with module boundary rules
```

## 🏷️ Understanding Tags

This repository uses tags to enforce module boundaries:

| Package        | Tag             | Can Import From        |
| -------------- | --------------- | ---------------------- |
| `@org/utils`   | `scope:shared`  | Nothing (base library) |
| `@org/strings` | `scope:strings` | `scope:shared`         |
| `@org/async`   | `scope:async`   | `scope:shared`         |
| `@org/colors`  | `scope:colors`  | `scope:shared`         |

The ESLint configuration enforces these boundaries, preventing circular dependencies and maintaining clean architecture.

## 🧪 Testing Module Boundaries

To see module boundary enforcement in action:

1. Try importing `@org/colors` into `@org/strings`
2. Run `npx nx run @org/strings:lint`
3. You'll see an error about violating module boundaries

## 📚 Useful Commands

```bash
# Project exploration
npx nx graph                                    # Interactive dependency graph
npx nx list                                     # List installed plugins
npx nx show project @org/strings --web              # View project details

# Development
npx nx run @org/strings:build                           # Build a specific package
npx nx run @org/async:test                              # Test a specific package
npx nx run @org/colors:lint                             # Lint a specific package

# Running multiple tasks
npx nx run-many -t build                       # Build all projects
npx nx run-many -t test --parallel=3          # Test in parallel
npx nx run-many -t lint test build            # Run multiple targets

# Affected commands (great for CI)
npx nx affected -t build                       # Build only affected projects
npx nx affected -t test                        # Test only affected projects

# Release management
npx nx release --dry-run                       # Preview release changes
npx nx release                                 # Create a new release
```

## Nx Cloud

Nx Cloud ensures a [fast and scalable CI](https://nx.dev/nx-cloud?utm_source=nx_project&utm_medium=readme&utm_campaign=nx_projects) pipeline. It includes features such as:

- [Remote caching](https://nx.dev/docs/features/ci-features/remote-cache?utm_source=nx_project&utm_medium=readme&utm_campaign=nx_projects)
- [Task distribution across multiple machines](https://nx.dev/docs/features/ci-features/distribute-task-execution?utm_source=nx_project&utm_medium=readme&utm_campaign=nx_projects)
- [Automated e2e test splitting](https://nx.dev/docs/features/ci-features/split-e2e-tasks?utm_source=nx_project&utm_medium=readme&utm_campaign=nx_projects)
- [Task flakiness detection and rerunning](https://nx.dev/docs/features/ci-features/flaky-tasks?utm_source=nx_project&utm_medium=readme&utm_campaign=nx_projects)

## Install Nx Console

Nx Console is an editor extension that enriches your developer experience. It lets you run tasks, generate code, and improves code autocompletion in your IDE. It is available for VSCode and IntelliJ.

[Install Nx Console &raquo;](https://nx.dev/docs/getting-started/editor-setup?utm_source=nx_project&utm_medium=readme&utm_campaign=nx_projects)

## 🔗 Learn More

- [Nx Documentation](https://nx.dev/docs)
- [Crafting Your Workspace Tutorial](https://nx.dev/docs/getting-started/tutorials/crafting-your-workspace)
- [Module Boundaries](https://nx.dev/docs/features/enforce-module-boundaries)
- [Releasing Packages](https://nx.dev/docs/features/manage-releases)
- [Nx Cloud](https://nx.dev/nx-cloud)

## 💬 Community

Join the Nx community:

- [Discord](https://go.nx.dev/community)
- [X (Twitter)](https://twitter.com/nxdevtools)
- [LinkedIn](https://www.linkedin.com/company/nrwl)
- [YouTube](https://www.youtube.com/@nxdevtools)
- [Blog](https://nx.dev/blog)
