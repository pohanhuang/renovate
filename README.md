# Dependency Automation

Shared Renovate configuration for repositories that want consistent dependency update rules.

## What This Repo Does

This repository centralizes Renovate settings so other repositories can reuse the same update policy instead of maintaining their own rules.

Current defaults include:

- **Security-only updates**: Only dependencies with known vulnerabilities will be updated (need manual review)
- All non-security updates (patch, minor, major) are disabled by default
- OSV vulnerability database integration enabled via `osvVulnerabilityAlerts`
- Disable some risky or manually managed updates such as `Longhorn`, `kubevirt`, Helm, and Go major bumps
- Group related dependencies into a single PR, such as:
  - `golang toolchain`
  - `SUSE BCI base images`
  - `k8s + rancher dependencies`

## Supported Managers

- `gomod`
- `dockerfile`
- `github-actions`
- `pip_requirements`

## Branch Policy

- `main` and `master`: normal update flow
- Release branches matching `v*`: not scanned by default; if a repository opts in via `baseBranchPatterns`, only patch and security updates are enabled

## Usage

In a repository that uses this shared config, extend it from `renovate.json`:

```json
{
  "extends": [
    "github>harvester/dependency-automation"
  ]
}
```

Add repo-specific overrides locally if needed.

## Main Config

The shared Renovate configuration lives in [renovate.json](./renovate.json).
