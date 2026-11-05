<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="logo-dark.svg">
  <img src="logo.svg" alt="HotCodePush" width="300">
</picture>

# HotCodePush

**Over-the-air updates for mobile apps.**

[Website](https://hotcodepush.com) · [Documentation](https://hotcodepush.com/docs) · [Discord](https://discord.gg/c5tTRAk2qW)

</div>

---

## What it is

HotCodePush is the over-the-air (OTA) update service for React Native, Expo, Capacitor and Cordova: the standard way to ship code updates to installed apps.
It is built by the team behind Capawesome, on the architecture that already delivers OTA updates at scale.

- JavaScript and asset changes reach installed apps with no store review in between.
- 1,000 monthly active devices (MAU) free, no credit card required.
- Pay-as-you-go at $1 per 1,000 MAU, from $5 a month, with a spending cap you set.
- 99.9% uptime on every paid plan, measured separately for update delivery and for the control plane.

[Pricing](https://hotcodepush.com/pricing) · [What is hot code push](https://hotcodepush.com/docs/concepts/what-is-hot-code-push)

## SDKs

One repository per framework, every SDK MIT.

- **React Native**: [`react-native-code-push`](https://github.com/hotcodepush-team/react-native-code-push) · [hotcodepush.com/react-native-code-push](https://hotcodepush.com/react-native-code-push)
- **Expo**: [`expo-ota-updates`](https://github.com/hotcodepush-team/expo-ota-updates) · [hotcodepush.com/expo-ota-updates](https://hotcodepush.com/expo-ota-updates)
- **Capacitor**: [`capacitor-live-updates`](https://github.com/hotcodepush-team/capacitor-live-updates) · [hotcodepush.com/capacitor-live-updates](https://hotcodepush.com/capacitor-live-updates)
- **Cordova**: [`cordova-code-push`](https://github.com/hotcodepush-team/cordova-code-push) · [hotcodepush.com/cordova-code-push](https://hotcodepush.com/cordova-code-push)

NativeScript, Electron and Tauri come later.

## Tooling

- **CLI**: [`cli`](https://github.com/hotcodepush-team/cli). `npx hotcodepush init` detects the framework, signs you in, creates the app and ships the first release. [CLI reference](https://hotcodepush.com/docs/cli)
- **CI/CD**: [`release-action`](https://github.com/hotcodepush-team/release-action), the GitHub Action around the CLI, and one recipe each for GitHub Actions, GitLab CI/CD, Bitbucket Pipelines and Azure DevOps, so every commit on `main` is an OTA update. [Ship from CI](https://hotcodepush.com/docs/ci)
- **MCP server**: `mcp.hotcodepush.com` connects an agent to the documentation and, with an API token, to the platform API. [MCP server](https://hotcodepush.com/docs/ai/mcp)
- **Agent skills**: `hotcodepush-init`, `hotcodepush-release`, `hotcodepush-migrate` and `hotcodepush-debug-no-update`, the skills a customer's agent installs. [Set up with an AI agent](https://hotcodepush.com/docs/ai)

## Migrating from CodePush or Appflow

Coming from App Center CodePush or Ionic Appflow, you are home.
The CodePush guide puts the React Native SDK in place of the CodePush client at your app's next native release, and you keep delta updates: precomputed deltas on every framework, with the main JavaScript bundle travelling as a byte-level patch.
The Appflow guide names the fork: Capawesome Cloud for the all-in-one shape with native builds and store publishing, HotCodePush for OTA depth.

[Migrate from CodePush](https://hotcodepush.com/docs/migrate/codepush) · [Migrate from Ionic Appflow](https://hotcodepush.com/docs/migrate/ionic-appflow)

## Connect

[Website](https://hotcodepush.com) · [Discord](https://discord.gg/c5tTRAk2qW) · [X](https://x.com/hotcodepush) · [Reddit](https://www.reddit.com/r/hotcodepush/) · [Newsletter](https://hotcodepush.com/newsletter)
