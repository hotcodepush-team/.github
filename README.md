# .github

The configuration repository of the `hotcodepush-team` organization: the org profile, the community health files, the default issue forms and the pull request template, the label manifests, the reusable workflows and the developer skills.
Everything in it applies to every repository of the organization that carries no file of its own.

## Development

There is nothing to build. Two checks before a push:

```
actionlint                     # every workflow
npx js-yaml <file> >/dev/null  # every manifest or issue form you touched
```

GitHub rejects a malformed issue form silently, so file a test issue through a form you changed.

## Deployment

A push to `main` is the deployment. GitHub picks up the profile, the health files and the templates immediately; the label manifests and the reusable workflows reach other repositories on their next run.

This repository's own automation runs from `.github/workflows/`:

| Workflow | Trigger | Does |
|---|---|---|
| `labels.yml` | weekly, on a manifest push, manual | syncs this repository's labels from the local manifests |
| `contributions.yml` | called | the pull request checks, `assign me`, the daily sweep |
| `stale.yml` | called | 21 idle days to `stale`, seven more to close |
| `contributions-caller.yml`, `stale-caller.yml` | events, schedule | this repository's own callers of the two |

## For other repositories

Copy these into the repository. They need no secret: each workflow's own `GITHUB_TOKEN` is enough.

### Label sync

`.github/workflows/labels.yml`, pulling the sets the repository uses by URL. Add the manifest lines the repository needs — `release.yml` where it publishes an artifact, `platform-mobile.yml` for a client SDK, `platform-desktop.yml` for the CLI, `area.yml` for the monorepo.

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
    - cron: '0 6 * * 1'
  push:
    branches: [main]
    paths: ['.github/workflows/labels.yml']
permissions:
  issues: write
jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: EndBug/label-sync@v2
        with:
          delete-other-labels: ${{ inputs.prune }}
          config-file: |
            https://raw.githubusercontent.com/hotcodepush-team/.github/main/labels/common.yml
            https://raw.githubusercontent.com/hotcodepush-team/.github/main/labels/release.yml
```

The raw URLs resolve once this repository is public. While it is private they return 404, so this repository syncs its own labels from a checkout instead — see `.github/workflows/labels.yml` here.

Run the prune once after a repository is created, to drop GitHub's defaults:

```
gh workflow run labels.yml -R hotcodepush-team/<repo> -f prune=true
```

### Contributions

`.github/workflows/contributions.yml`:

```yaml
name: Contributions
on:
  pull_request_target:
    types: [opened, edited, reopened, synchronize]
  issue_comment:
    types: [created]
  schedule:
    - cron: '30 5 * * *'
permissions:
  contents: read
  issues: write
  pull-requests: write
jobs:
  contributions:
    uses: hotcodepush-team/.github/.github/workflows/contributions.yml@main
```

### Stale

`.github/workflows/stale.yml`:

```yaml
name: Stale
on:
  schedule:
    - cron: '30 4 * * *'
  workflow_dispatch:
permissions:
  contents: read
  issues: write
  pull-requests: write
jobs:
  stale:
    uses: hotcodepush-team/.github/.github/workflows/stale.yml@main
```

Both callers reach a reusable workflow in a private repository only while this repository's Actions access allows the organization; once it is public, nothing is needed.

### Skills

```
npx skills add hotcodepush-team/.github
npx skills add hotcodepush-team/.github --skill triage-issue
```

The skills land in the repository's `.claude/skills/` and are pinned in its `skills-lock.json`. Commit both.

## Handbook

The plan behind every file here — the label rules, the template decisions, the org profile's sections, the workflow catalog — lives in the handbook: `agents.md` for the labels, the templates and the agent workspaces, `repositories.md` for the workflows, the README rules and licensing.

## License

See [LICENSE](./LICENSE).
