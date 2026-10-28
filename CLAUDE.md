# hotcodepush-team/.github

The organization's configuration repository.
GitHub reads it: the org profile, the community health files every other repository inherits, the default issue forms and the pull request template.
We read it too: the label manifests, the reusable workflows and the developer skills every repository pulls from here.

Nothing here is a product. Every file is either read by GitHub at a fixed path or copied into other repositories, so a path is an interface and a rename is a breaking change.

## What lives where

| Path | What it is | Who reads it |
|---|---|---|
| `profile/README.draft.md` | the organization's front page, held back until launch; GitHub shows it once it is `profile/README.md` | GitHub, at `github.com/hotcodepush-team` |
| `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md` | the community health files | every org repository without its own copy |
| `.github/ISSUE_TEMPLATE/` | the three forms and the chooser | every org repository without its own `ISSUE_TEMPLATE` folder |
| `.github/PULL_REQUEST_TEMPLATE.md` | the pull request template | every org repository, always; it is never overridden |
| `labels/*.yml` | the label sets | every repository's `labels.yml` workflow |
| `.github/workflows/contributions.yml`, `labels.yml`, `stale.yml` | reusable workflows | every repository's caller of the same name |
| `skills/*/SKILL.md` | the developer skills | every repository's `.claude/skills/`, via the skills CLI |
| `.github/workflows/*-caller.yml`, `labels-local.yml` | this repository's own callers and its own label sync | this repository only |

No `.mcp.json` here: this repository has no stack, so no MCP server earns its context.

## Changing a label

Labels change in the manifests under `labels/`, never in a repository's settings.
That is the rule that keeps a prune safe.

1. Edit the set's YAML file. `name`, `color` (six hex digits, quoted, no `#`) and `description` (at most 100 characters).
2. Push to `main`. Every repository's weekly run and the push trigger create and update labels, so the change reaches the org within a week without deleting anything.

**Renaming** a label uses `aliases`, never a delete and a create — the alias renames the existing label and keeps every issue on it:

```yaml
- name: type/perf
  color: '0e8a16'
  description: Performance improvement
  aliases: ['performance']
```

Leave the alias in place for one prune cycle across every repository, then remove it.

**Pruning** deletes every label a repository carries that no manifest defines.
It removes the label from every issue that carries it and cannot be undone, so it is never automatic:

```
gh workflow run labels.yml -R hotcodepush-team/<repo> -f prune=true
```

Run it once per repository, right after creation, to drop GitHub's defaults — and again only after a label was removed from a manifest.

## Changing a form or the pull request template

The forms live in `.github/ISSUE_TEMPLATE/`.
GitHub rejects a malformed form silently — the form simply stops appearing in the chooser — so parse the YAML before pushing, and file a test issue through the changed form afterwards.

Rules the forms carry and must keep carrying:

- Every form applies `state/needs-triage`, and `bug_report` and `feature_request` also apply their `type/*`. The Idea form applies `idea` instead of a type.
- A label a form applies has to exist in `labels/common.yml`, or GitHub drops it without a word.
- `title` carries the conventional-commit prefix with its trailing space: `'bug: '`, `'feat: '`, `'idea: '`.
- The before-submitting checkboxes are required. They are the reason the first reply is unnecessary.

Client SDK repositories override these forms with their own copies; a change here does not reach them.

## Changing a skill

One folder per skill under `skills/`, one `SKILL.md` each, [agentskills.io](https://agentskills.io) format: frontmatter with `name` matching the folder and `description` saying what the skill does and when to use it, then the instructions.

A skill is public and is copied into public repositories.
Nothing about how we work internally, no private scope, no customer, no credential.

After a change, each repository picks it up with a skills update run and a commit of its own — Claude Code reads only the copy in the repository it is opened in, never this one.

## How other repositories consume this repository

| What | How |
|---|---|
| Labels | a `labels.yml` caller naming its sets, with `secrets: inherit`; the template is in the [README](README.md) |
| Contributions and stale | a caller workflow with `uses: hotcodepush-team/.github/.github/workflows/<name>.yml@main`; the templates are in the [README](README.md) |
| Skills | `npx skills add hotcodepush-team/.github`, pinned in that repository's `skills-lock.json` |
| Health files, forms, the pull request template | nothing to do; GitHub falls back to this repository on its own |

Both reusable workflows read metadata only and never check out pull request code.
Changing one changes every repository at the next run, so treat a change to `contributions.yml` as a change to every repository's merge gate.

## Working here

- Trunk-based: small conventional commits straight to `main`, no pull requests.
- Validate before pushing: `actionlint` over `.github/workflows/`, and a YAML parse over every manifest and form.
- Never commit a secret, a token, a customer name or a customer identifier.
- The plan this repository implements lives in the handbook, not here.
