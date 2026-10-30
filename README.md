# Nuvio TV for TizenBrew (bundled, no hosted server)

Unofficial TizenBrew module that serves the Nuvio TV Tizen build **from this repository** instead of
`https://web.nuvioapp.space`, so it works while the hosted server is unavailable and on Samsung
Tizen 4 TVs (2018) that reject the standalone WGT with `install failed[118012]`.

- Source: [NuvioMedia/NuvioTVSmart](https://github.com/NuvioMedia/NuvioTVSmart), release
  [1.2.10](https://github.com/NuvioMedia/NuvioTVSmart/releases/tag/1.2.10) (`NuvioTV-Tizen-1.2.10.wgt`).
- Changes: removed `services/` and `config.xml`; removed the inline `wrt:service` import from
  `index.html`; set `__NUVIO_TIZEN_ENGINEFS_SERVICE_ENABLED__` and
  `__NUVIO_TIZEN_PLUGIN_SERVICE_ENABLED__` to `false` in `main.js`. Torrent/P2P and plugins are
  therefore unavailable (Tizen 4 does not support them anyway).
- TizenBrew modules have no access to Samsung AVPlay (`webapis`). `app.bundle.js` is patched so a
  direct file source falls back to the HTML5 `<video>` player when AVPlay is unavailable, instead of
  failing with `AVPlay startup failed before prepareAsync`. Sources that need request headers
  (Referer/Cookie) still cannot play without the local proxy service.
- License: GPL-3.0, same as the original (see `LICENSE`).

## Install
In TizenBrew add the GitHub module:

```text
nvidiaqwer/nuvio-tizenbrew-local@main
```

`@main` always loads the latest commit; without it jsDelivr may keep serving an older version for hours.
