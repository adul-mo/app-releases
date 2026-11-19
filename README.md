# App releases

Installers and update feeds for several Windows apps. Source code lives elsewhere; this repo only holds releases, so apps can update themselves without a token.

## Layout

Every app uses its own tag prefix (`<app>`, e.g. `zerodupe`):

| Release | Contains | Used by |
|---|---|---|
| `<app>-latest` | `latest.yml`, `beta.yml` and the newest installer(s) | the app's auto-updater |
| `<app>-v<version>` | the installer for that version | people downloading it by hand |

- `latest.yml` points at the newest **stable** version.
- `beta.yml` points at the newest version, stable or test. Apps switch to it when "receive test versions" is on.
- Only the newest 2 `<app>-v*` releases of each app are kept.

## Adding an app

1. In the app's `electron-builder.yml`:

   ```yaml
   publish:
     - provider: generic
       url: https://github.com/adul-mo/app-releases/releases/download/<app>-latest
   ```

2. Copy `scripts/release.mjs` from Zerodupe. It reads the URL above to find this repo and the app's prefix, and only ever changes that app's releases.
3. Run `npm run release` (optionally `-- --notes notes.md`).

## Apps

| App | Download |
|---|---|
| Zerodupe | [latest](https://github.com/adul-mo/app-releases/releases?q=zerodupe-v) |
