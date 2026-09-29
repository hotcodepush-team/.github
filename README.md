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
| `labels.yml` | called | syncs the caller's labels from the manifests here |
| `labels-local.yml` | weekly, on a manifest push, manual | syncs this repository's labels from the local manifests |
| `contributions.yml` | called | the pull request checks, `assign me`, the daily sweep |
| `stale.yml` | called | 21 idle days to `stale`, seven more to close |
| `contributions-caller.yml`, `stale-caller.yml` | events, schedule | this repository's own callers of the two |

## For other repositories

Copy these into the repository. None of them needs a secret, the workflow's own `GITHUB_TOKEN` is enough. The label sync caller stays disabled until this repository is public, since the manifests are read from here.

### Label sync

`.github/workflows/labels.yml`, naming the sets the repository uses in `sets` — `common` everywhere, plus `release` where it publishes an artifact, `platform-mobile` for a client SDK, `platform-desktop` for the CLI, `area` for the monorepo.

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
    uses: hotcodepush-team/.github/.github/workflows/labels.yml@main
    with:
      sets: common release
      prune: ${{ inputs.prune == true }}
    secrets: inherit
```

The reusable workflow checks this repository out and syncs the caller's labels with the caller's own `GITHUB_TOKEN`, which works once this repository is public; until then every caller stays disabled and no sync runs.
Until both secrets are set, it prints a notice and syncs nothing.
This repository syncs its own labels from a plain checkout instead — see `.github/workflows/labels-local.yml`.

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

The three callers reach a reusable workflow in a private repository only while this repository's Actions access allows the organization; once it is public, nothing is needed.

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
