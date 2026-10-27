# Shasta app releases

Signed [Isolated Web App](https://developer.chrome.com/docs/iwa) bundles for **Shasta**
(`.swbn`), and the update manifest administrators use. Nothing here needs a server: the files are
static and the bundle is signed, so Chrome verifies it before installing.

Built from the private source repo (Shasta is AGPL-3.0).

## Install (personal computer or Chromebook)

1. Download the newest `shasta-<version>.swbn` from the [latest release](../../releases/tag/app-latest).
2. Open the downloaded file (on a Chromebook: Files → Downloads, double-click it).
   Chrome 150+ installs it directly. Older Chrome: enable
   `chrome://flags/#enable-isolated-web-app-unmanaged-install`, relaunch, then open the file — or use
   `chrome://web-app-internals` → *Install IWA from Signed Web Bundle*.

The app runs on its own `isolated-app://` origin, with no relay server.

## Administrators

`update.json` is a Web Application Update Manifest. Add the app in the Google Admin console
(Devices → Chrome → Apps & extensions → Isolated Web App) with:

- **Web Bundle ID:** `domblmy72no3gihfrsnkhpedixfdwr5oa3px6gpd75hmu3s7qs5qaaic`
- **Update manifest URL:** `https://github.com/dazacode/shasta-releases/releases/download/app-latest/update.json`

## Publishing a new version

```sh
IWA_BASE_URL=https://github.com/dazacode/shasta-releases/releases/download/app-latest/ bun run build:iwa
gh release upload app-latest --repo dazacode/shasta-releases --clobber \
  .iwa/publish/shasta-<version>.swbn .iwa/publish/update.json
```
