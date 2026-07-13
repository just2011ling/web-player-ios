# Tauri + Vue + TypeScript

This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Vue - Official](https://marketplace.visualstudio.com/items?itemName=Vue.volar) + [Tauri](https://marketplace.visualstudio.com/items?itemName=tauri-apps.tauri-vscode) + [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer)

## iOS Build With GitHub Actions

This repository includes [.github/workflows/ios-build.yml](.github/workflows/ios-build.yml) to build a signed iOS IPA on a macOS GitHub Actions runner.

### Trigger

Run the `ios-build` workflow manually from the GitHub Actions tab and choose one of these export methods:

- `debugging`
- `release-testing`
- `app-store-connect`

### Required Secrets

You must configure one of the following signing modes before the workflow can succeed. Without these secrets, the workflow will fail fast and no IPA will be produced.

Automatic signing with App Store Connect API key:

- `APPLE_API_ISSUER`
- `APPLE_API_KEY`
- `APPLE_API_KEY_CONTENT`

Manual signing with certificate and provisioning profile:

- `IOS_CERTIFICATE`
- `IOS_CERTIFICATE_PASSWORD`
- `IOS_MOBILE_PROVISION`

Notes:

- `APPLE_API_KEY` is the App Store Connect key ID.
- `APPLE_API_KEY_CONTENT` is the full contents of the downloaded `.p8` file.
- `IOS_CERTIFICATE` and `IOS_MOBILE_PROVISION` must be base64-encoded values.
- The bundle identifier in [src-tauri/tauri.conf.json](src-tauri/tauri.conf.json) must match the App ID you created in Apple Developer.
- For GitHub Actions IPA output, the recommended path is automatic signing with `APPLE_API_ISSUER`, `APPLE_API_KEY`, and `APPLE_API_KEY_CONTENT`.

### Local macOS Commands

If you want to initialize or build iOS locally on macOS, use:

```bash
npm run tauri:ios:init -- --ci
npm run tauri:ios:build -- --ci --target aarch64 --export-method release-testing
```

The iOS CLI commands are only available on macOS hosts, so they will not run on Windows.
