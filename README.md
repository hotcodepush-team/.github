# .github

The configuration repository of the `hotcodepush-team` organization: the org profile, the community health files, the issue forms and the pull request template, the label manifests, the reusable workflows and the developer skills.
Everything in it applies to every repository of the organization that carries no file of its own.

## Project structure

```
profile/                   the org profile README and logos
CONTRIBUTING.md, CODE_OF_CONDUCT.md, SECURITY.md   the default community health files
.github/ISSUE_TEMPLATE/    the default issue forms
.github/PULL_REQUEST_TEMPLATE.md
.github/workflows/         the reusable workflows and this repository's own callers
labels/                    the label manifests, one set per file
skills/                    the developer skills: create-pr, resolve-issue, review-pr, triage-issue, validate-issue
```

## Development

There is nothing to build. Two checks before a push:

```sh
actionlint                     # every workflow
npx js-yaml <file> >/dev/null  # every manifest or issue form you touched
```

GitHub rejects a malformed issue form silently, so file a test issue through a form you changed.

## Deployment

A push to `main` is the deployment: GitHub picks up the profile, the health files and the templates immediately, and the label manifests and the reusable workflows reach other repositories on their next run.

| Workflow                                       | Trigger                            | Does                                                    |
| ---------------------------------------------- | ---------------------------------- | ------------------------------------------------------- |
| `labels.yml`                                   | called                             | syncs the caller's labels from the manifests here       |
| `labels-local.yml`                             | weekly, on a manifest push, manual | syncs this repository's labels from the local manifests |
| `contributions.yml`                            | called                             | the pull request checks, `assign me`, the daily sweep   |
| `stale.yml`                                    | called                             | 21 idle days to `stale`, seven more to close            |
| `contributions-caller.yml`, `stale-caller.yml` | events, schedule                   | this repository's own callers of the two                |

## Usage in other repositories

Copy the three callers below into the repository's `.github/workflows/`; none needs a secret.
A private repository can call them only while this repository's Actions access allows the organization; once it is public, nothing is needed.

`labels.yml` names the label sets the repository uses in `sets`: `common` everywhere, plus `release` where it publishes an artifact, `platform-mobile` for a client SDK, `platform-desktop` for the CLI, `area` and `device-tests` for the monorepo.
It stays disabled until this repository is public, since the manifests are read from here.

```yaml
name: Sync labels
on:
  workflow_dispatch:
    inputs:
      prune:
        description: Delete labels that are not in the manifests
        type: boolean
        default: false
  schedule:
    - cron: "0 6 * * 1"
  push:
    branches: [main]
    paths: [".github/workflows/labels.yml"]
permissions:
  issues: write
jobs:
  sync:
    uses: hotcodepush-team/.github/.github/workflows/labels.yml@main
    with:
      sets: common release
      prune: ${{ inputs.prune == true }}
```

Run the prune once after a repository is created, to drop GitHub's defaults: `gh workflow run labels.yml -R hotcodepush-team/<repo> -f prune=true`.

`contributions.yml` and `stale.yml` take no inputs:

```yaml
name: Contributions
on:
  pull_request_target:
    types: [opened, edited, reopened, synchronize]
  issue_comment:
    types: [created]
  schedule:
    - cron: "30 5 * * *"
permissions:
  contents: read
  issues: write
  pull-requests: write
jobs:
  contributions:
    uses: hotcodepush-team/.github/.github/workflows/contributions.yml@main
```

```yaml
name: Stale
on:
  schedule:
    - cron: "30 4 * * *"
  workflow_dispatch:
permissions:
  contents: read
  issues: write
  pull-requests: write
jobs:
  stale:
    uses: hotcodepush-team/.github/.github/workflows/stale.yml@main
```

The developer skills land in a repository's `.claude/skills/` and are pinned in its `skills-lock.json`; commit both:

```sh
npx skills add hotcodepush-team/.github
npx skills add hotcodepush-team/.github --skill triage-issue
```

## Handbook

| Topic                                           | Doc                    |
| ----------------------------------------------- | ---------------------- |
| The labels, the templates, the agent workspaces | `docs/agents.md`       |
| The workflows, the README rules, licensing      | `docs/repositories.md` |

## License

See [LICENSE](./LICENSE).
