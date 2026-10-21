<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="logo-dark.svg">
  <img src="logo.svg" alt="HotCodePush" width="300">
</picture>

# HotCodePush

**Hot code push for every app.**

[Website](https://hotcodepush.com) · [Documentation](https://hotcodepush.com/docs) · [Discussions](https://github.com/orgs/hotcodepush-team/discussions)

</div>

---

## What it is

HotCodePush is the open platform for over-the-air code updates — the standard way to ship code updates to Capacitor, Cordova, React Native and Expo apps.
It is built by the team behind Capawesome, on the architecture that already delivers live updates at scale.

- JavaScript and asset changes reach installed apps in about a minute, with no store review in between.
- 1,000 monthly active devices (MAU) free, no credit card required.
- Pay-as-you-go at $1 per 1,000 MAU, from $5 a month, with a spending cap you set.
- 99.9% uptime committed on every paid plan, for update delivery and for the control plane.

[Pricing](https://hotcodepush.com/pricing) · [What is hot code push](https://hotcodepush.com/docs/concepts/what-is-hot-code-push)

## SDKs

One repository per framework, every SDK MIT.

- **Capacitor** — [`capacitor-live-updates`](https://github.com/hotcodepush-team/capacitor-live-updates) · [hotcodepush.com/capacitor-live-updates](https://hotcodepush.com/capacitor-live-updates)
- **React Native** — [`react-native-code-push`](https://github.com/hotcodepush-team/react-native-code-push) · [hotcodepush.com/react-native-code-push](https://hotcodepush.com/react-native-code-push)
- **Expo** — [`expo-ota-updates`](https://github.com/hotcodepush-team/expo-ota-updates) · [hotcodepush.com/expo-ota-updates](https://hotcodepush.com/expo-ota-updates)
- **Cordova** — [`cordova-code-push`](https://github.com/hotcodepush-team/cordova-code-push) · [hotcodepush.com/cordova-code-push](https://hotcodepush.com/cordova-code-push)

NativeScript, Electron and Tauri come later.

## Tooling

- **CLI** — [`cli`](https://github.com/hotcodepush-team/cli). `npx hotcodepush init` detects the framework, signs you in, creates the app and ships the first release: under sixty seconds from `init` to a live update. [CLI reference](https://hotcodepush.com/docs/cli)
- **CI/CD** — [`release-action`](https://github.com/hotcodepush-team/release-action), the GitHub Action around the CLI, and one recipe each for GitHub Actions, GitLab CI/CD, Bitbucket Pipelines and Azure DevOps, so every commit on `main` is a live update. [Ship from CI](https://hotcodepush.com/docs/ci)
- **MCP server** — [`mcp`](https://github.com/hotcodepush-team/mcp) connects an agent to the documentation and, with an API token, to the platform API.
- **Agent skills** — [`skills`](https://github.com/hotcodepush-team/skills): `hotcodepush-init`, `hotcodepush-release` and `hotcodepush-debug-no-update`, the three skills a customer's agent installs. [Set up with an AI agent](https://hotcodepush.com/docs/ai)

## Migrating from CodePush or Appflow

Coming from App Center CodePush or Ionic Appflow, you are home.
The CodePush guide puts the React Native SDK in place of the CodePush client at your app's next native release, and you keep delta updates: precomputed delta packs with the main bundle inside as a byte-level patch, typically smaller than file-level diffs.
The Appflow guide names the fork: Capawesome Cloud for the all-in-one shape with native builds and store publishing, HotCodePush for OTA depth.

[Migrate from CodePush](https://hotcodepush.com/docs/migrate/codepush) · [Migrate from Ionic Appflow](https://hotcodepush.com/docs/migrate/ionic-appflow)

## Connect

[Website](https://hotcodepush.com) · [Discussions](https://github.com/orgs/hotcodepush-team/discussions) · [Newsletter](https://hotcodepush.com/newsletter)

<!-- TODO: the social profiles, once the handles are decided — X · LinkedIn · YouTube · Discord -->
