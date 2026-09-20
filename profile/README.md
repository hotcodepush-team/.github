<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="logo-dark.svg">
  <img src="logo.svg" alt="HotCodePush" width="300">
</picture>

# HotCodePush

**Hot code push for every app.**

[Website](https://hotcodepush.com) · [Documentation](https://hotcodepush.com/docs) · [Blog](https://hotcodepush.com/blog) · [Discussions](https://github.com/orgs/hotcodepush-team/discussions)

</div>

---

## What it is

HotCodePush is the open platform for over-the-air code updates — the standard way to ship code updates to Capacitor, Cordova, React Native and Expo apps.
It is built by the team behind Capawesome, on the architecture that already delivers live updates at scale.

- JavaScript and asset changes reach installed apps in about a minute, with no store review in between.
- 1,000 monthly active users free, no credit card.
- $1 per 1,000 monthly active users after that, from $5 a month, with a spending cap you set.
- 99.9% uptime committed on both surfaces — update delivery and the control plane — on every paid plan.

[Pricing](https://hotcodepush.com/pricing) · [How an update is delivered](https://hotcodepush.com/docs/concepts/what-is-hot-code-push)

## SDKs

One repository per framework, all MIT.

| Framework | SDK | Guide |
|---|---|---|
| Capacitor | [`capacitor-live-updates`](https://github.com/hotcodepush-team/capacitor-live-updates) | [Capacitor live updates](https://hotcodepush.com/capacitor-live-updates) |
| React Native | [`react-native-code-push`](https://github.com/hotcodepush-team/react-native-code-push) | [React Native CodePush](https://hotcodepush.com/react-native-code-push) |
| Expo | [`expo-ota-updates`](https://github.com/hotcodepush-team/expo-ota-updates) | [Expo OTA updates](https://hotcodepush.com/expo-ota-updates) |
| Cordova | [`cordova-code-push`](https://github.com/hotcodepush-team/cordova-code-push) | [Cordova code push](https://hotcodepush.com/cordova-code-push) |

Electron, Tauri and Flutter follow after launch.

## Tooling

- **CLI** — [`cli`](https://github.com/hotcodepush-team/cli). `npx hotcodepush init` goes from sign-in to the first live update. [Reference](https://hotcodepush.com/docs/cli)
- **CI/CD** — every commit on `main` as a live update, with recipes for GitHub Actions, GitLab CI/CD, Bitbucket Pipelines and Azure DevOps. [Ship from CI](https://hotcodepush.com/docs/ci)
- **MCP server** — [`mcp`](https://github.com/hotcodepush-team/mcp) gives an agent the documentation and the platform API.
- **Agent skills** — [`skills`](https://github.com/hotcodepush-team/skills) sets a project up, ships a release and debugs a device that did not update. [Set up with an AI agent](https://hotcodepush.com/docs/ai)
- **Typed clients** — [`hotcodepush-node`](https://github.com/hotcodepush-team/hotcodepush-node) and [`hotcodepush-python`](https://github.com/hotcodepush-team/hotcodepush-python), both generated against the published OpenAPI spec.

## Migrating from CodePush or Appflow

Coming from App Center CodePush or Ionic Appflow, you are home.
Existing CodePush clients change a URL; the concepts you already use — deployments, targeted binary versions, mandatory updates, staged rollouts, rollbacks — keep their names and their behavior.
Both guides are written as a checklist, with the differences named where they exist rather than glossed over.

[Migrate from CodePush](https://hotcodepush.com/docs/migrate/codepush) · [Migrate from Ionic Appflow](https://hotcodepush.com/docs/migrate/ionic-appflow)

## Latest from the blog

The blog opens with the launch, at [hotcodepush.com/blog](https://hotcodepush.com/blog).
Every shipped feature also gets an entry in the [changelog](https://hotcodepush.com/changelog).

## Connect

[Website](https://hotcodepush.com) · [Discussions](https://github.com/orgs/hotcodepush-team/discussions) · [Changelog](https://hotcodepush.com/changelog) · [Status](https://status.hotcodepush.com) · [Newsletter](https://hotcodepush.com/newsletter)
