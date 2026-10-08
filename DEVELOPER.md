# Developer Guide: Google Data Cloud Plugins

This document provides instructions for developers contributing to the Google Data Cloud Plugins.

## Prerequisites

*   **Git:** Required for cloning and managing submodules.
*   **Gemini CLI:** Ensure you have version `v0.6.0` or above to test extensions locally.
*   **Python 3.9+:** (Optional) Required if you are running `evalbench` from the `agent-evaluation` directory.

## Developing the Kit

### 1. Clone the Repository and Submodules

When cloning this repository for the first time, you need to initialize the submodules:

```bash
git clone --recurse-submodules https://github.com/googlecloudplatform/data-cloud-plugins.git
cd data-cloud-plugins
```

If you have already cloned the repository without submodules, initialize and update them:

```bash
git submodule update --init --recursive
```

### 2. Updating Submodules

To pull the latest changes for all product submodules (bringing them up to date with their respective remote `main` branches):

```bash
git submodule update --remote --merge
```

To pull the latest changes for a specific submodule:

```bash
cd <submodule-directory>
git pull origin main
```

To check the status of all submodules:
```bash
git submodule status
```

### 3. Testing Local Changes

If you are developing a new skill or modifying a tool within one of the submodules, you can install that specific extension locally into your Gemini CLI for testing:

```bash
gemini extensions install ./<submodule-directory>
```
*Note: Make sure to follow any specific binary download instructions required by the individual extension's `DEVELOPER.md` (e.g., downloading the `toolbox` binary).*

## Testing

*   **Skill Validation:** Ensure any new Skills follow the architectural guidelines outlined in the main design document (prescriptive feature selection, non-overlapping functionality, IP safety). Test your skills locally before submitting PRs.
*   **Agent Evaluation:** We recommend using [EvalBench](./agent-evaluation/README.md) to benchmark and safety-test changes to agent prompts and tools.
*   **Automated Checks:** Individual product repositories enforce their own automated presubmit checks (e.g., license headers, structural validation, GitHub Actions).

## Maintainer Information

### Conventional Commits
Please use [Conventional Commits](https://www.conventionalcommits.org/) for your pull requests. This ensures that automated changelogs and version bumps (via Release Please) are handled correctly across the ecosystem.

### Updating Submodule References

#### Automated Updates (Recommended)
This repository is configured with **Renovate** to automatically keep submodule references up to date with their latest stable releases and tags:
* **Unified PRs:** When a new branch version (e.g., `0.1.0` -> `0.2.0`) is found on a remote submodule, Renovate opens a single consolidated Pull Request bundling both the tracking branch update in `.gitmodules` and the new commit SHA (digest) together.
* **Semantic Commits:** These automated PRs and commits are prefixed with the `feat` type (e.g., `feat(deps): update alloydb submodule`).
* **Digest Filtering:** To reduce PR noise, Renovate will ignore pure digest-only updates if no new branch/version has been tagged or updated on the remote submodule.

#### Manual Updates (Backup / Fallback)
If you need to manually update the submodule pointers to reflect the latest stable releases of the product extensions:

1. Run `git submodule update --remote --merge --recursive`.
2. Commit the updated submodule hashes: `git commit -am "chore: update product submodules to latest"`.
3. Open a Pull Request to merge the updated pointers into `main`.

### Releasing
Individual product extensions currently manage their own automated releases (typically using Google's `release-please-action`). Check the `DEVELOPER.md` of the specific product repository for detailed release workflows and automated changelog enrichment.
