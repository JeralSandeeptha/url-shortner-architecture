# ADR 07: Use GitHub Actions for CI/CD Pipeline

## Status
Accepted

## Context
We needed to choose a CI/CD tool for automating build, test, and deployment workflows across the project.

Key considerations included:
- `Integration with Git Hosting`: Should integrate seamlessly with our repository hosting platform.
- `Developer Experience`: Workflows should be easy to configure, maintain, and debug.
- `Extensibility`: Should support reusable workflows, third-party actions, and custom scripts.
- `Cost & Performance`: Prefer a solution with good pricing, predictable performance, and minimal overhead.
- `Ecosystem & Community`: Availability of plugins, documentation, and support.

## Decision
We will use GitHub Actions as our CI/CD pipeline solution.

How we’ll do it:
- Use .github/workflows directory to store all workflow files.
- Configure pipelines for:
    - Build & Test on every push and pull request.
    - Linting and Type Checking using ESLint and TypeScript.
    - Automated Deployment to the selected environment (e.g., staging/production) when merging into main.
- Use GitHub Secrets to store API keys, environment variables, and deployment tokens.
- Use Reusable Workflows for shared pipeline steps like setup, caching, or test execution.
- Utilize official actions such as:
    - actions/checkout
    - actions/setup-node
    - actions/cache
    - Leverage caching to speed up installs (node_modules, TypeScript builds).

Example workflow structure:

- `ci.yml` → Build, test, lint
- `deploy.yml` → Deployment on main branch push
- `release.yml` → Automatic tagging, versioning, or publishing

## Consequences
Positive
- `Tight integration with GitHub repository`: PR checks, status badges, and inline results.
- Fast setup and minimal maintenance—no server or agent management.
- Large ecosystem of ready-made actions reduces custom scripting.
- Easily auditable workflow files committed to the repository.
- Scales well with the project using hosted or self-hosted runners.

Negative
- If workflows grow large, YAML files may become verbose and harder to maintain.
- Heavy usage could increase costs depending on minutes used.
- `Vendor lock-in`: workflows are not portable to other platforms.

## Alternatives Considered (optional)
- `GitLab CI`: Rejected because project repository is hosted in GitHub.
- `Jenkins`: Rejected due to maintenance overhead and complexity.
- `CircleCI`: Rejected due to separate platform overhead and unnecessary fragmentation.

## Date
2025-11-17

## Authors / Reviewers
DevOps Engineer
Backend Team Lead
Software Architect