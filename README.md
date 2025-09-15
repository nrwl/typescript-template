# Nx TypeScript Template Repository

<a alt="Nx logo" href="https://nx.dev" target="_blank" rel="noreferrer"><img src="https://raw.githubusercontent.com/nrwl/nx/master/images/nx-logo.png" width="45"></a>

✨ A template repository showcasing key [Nx](https://nx.dev) features for TypeScript monorepos ✨

## 📦 Project Overview

This template demonstrates a production-ready TypeScript monorepo with:

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
nx run-many -t build

# Run tests (note: one test intentionally fails for CI demo)
nx run-many -t test

# Lint all projects
nx run-many -t lint

# Run everything in parallel
nx run-many -t lint test build --parallel=3

# Visualize the project graph
nx graph
```

## ⭐ Featured Nx Capabilities

This template showcases several powerful Nx features:

### 1. 🔒 Module Boundaries

Enforces architectural constraints using tags. Each package has specific dependencies it can use:

- `scope:shared` (utils) - Can be used by all packages
- `scope:strings` - Can only depend on shared utilities
- `scope:async` - Can only depend on shared utilities
- `scope:colors` - Can only depend on shared utilities

**Try it out:**
```bash
# See the current project graph and boundaries
nx graph

# View a specific project's details
nx show project strings --web
```

[Learn more about module boundaries →](https://nx.dev/features/enforce-module-boundaries)

### 2. 🛠️ Custom Run Commands

Packages can define custom commands beyond standard build/test/lint:

```bash
# Run the custom build-base command for strings package
nx run strings:build-base

# See all available targets for a project
nx show project strings
```

[Learn more about custom run commands →](https://nx.dev/concepts/executors-and-configurations)

### 3. 🔧 Self-Healing CI

The CI pipeline includes `nx fix-ci` which automatically identifies and suggests fixes for common issues. We've included an intentionally failing test in the `@org/async` package to demonstrate this feature.

```bash
# Run tests and see the failure
nx test async

# In CI, this command provides automated fixes
npx nx fix-ci
```

[Learn more about self-healing CI →](https://nx.dev/ci/features/self-healing-ci)

### 4. 📦 Package Publishing

Manage releases and publishing with Nx Release:

```bash
# Dry run to see what would be published
nx release --dry-run

# Version and release packages
nx release

# Publish only specific packages
nx release publish --projects=strings,colors
```

[Learn more about Nx Release →](https://nx.dev/features/manage-releases)

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

| Package | Tag | Can Import From |
|---------|-----|----------------|
| `@org/utils` | `scope:shared` | Nothing (base library) |
| `@org/strings` | `scope:strings` | `scope:shared` |
| `@org/async` | `scope:async` | `scope:shared` |
| `@org/colors` | `scope:colors` | `scope:shared` |

The ESLint configuration enforces these boundaries, preventing circular dependencies and maintaining clean architecture.

## 🧪 Testing Module Boundaries

To see module boundary enforcement in action:

1. Try importing `@org/colors` into `@org/strings`
2. Run `nx lint strings`
3. You'll see an error about violating module boundaries

## 📚 Useful Commands

```bash
# Project exploration
nx graph                                    # Interactive dependency graph
nx list                                     # List installed plugins
nx show project strings --web              # View project details

# Development
nx build strings                           # Build a specific package
nx test async                              # Test a specific package
nx lint colors                             # Lint a specific package

# Running multiple tasks
nx run-many -t build                       # Build all projects
nx run-many -t test --parallel=3          # Test in parallel
nx run-many -t lint test build            # Run multiple targets

# Affected commands (great for CI)
nx affected -t build                       # Build only affected projects
nx affected -t test                        # Test only affected projects

# Release management
nx release --dry-run                       # Preview release changes
nx release                                 # Create a new release
```

## 🔗 Learn More

- [Nx Documentation](https://nx.dev)
- [Module Boundaries](https://nx.dev/features/enforce-module-boundaries)
- [Custom Commands](https://nx.dev/concepts/executors-and-configurations)
- [Self-Healing CI](https://nx.dev/ci/features/self-healing-ci)
- [Releasing Packages](https://nx.dev/features/manage-releases)
- [Nx Cloud](https://nx.dev/ci/intro/why-nx-cloud)

## 💬 Community

Join the Nx community:
- [Discord](https://go.nx.dev/community)
- [X (Twitter)](https://twitter.com/nxdevtools)
- [LinkedIn](https://www.linkedin.com/company/nrwl)
- [YouTube](https://www.youtube.com/@nxdevtools)
- [Blog](https://nx.dev/blog)