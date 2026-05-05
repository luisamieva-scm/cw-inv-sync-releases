# cw-inv-sync — Releases

Public release artifacts (Windows MSI installers) for **cw-inv-sync**, the
Copperweld inventory sync application.

> The application source code lives in a **private** repository. This
> repo only hosts the compiled installers so plant PCs can pull updates
> without authenticating to GitHub.

---

## Installing on a plant PC

1. Open the
   [latest release](https://github.com/luisamieva-scm/cw-inv-sync-releases/releases/latest)
   page in a browser.
2. Download the `cw-inv-sync_<version>_x64_en-US.msi` file.
3. Double-click the MSI to run it.
4. Windows SmartScreen will warn that the publisher is unverified — this
   is expected for v1 (code signing is on the roadmap). Click
   **More info → Run anyway**.
5. Follow the installer prompts.

## Updating an existing install

Same steps as a fresh install — the MSI handles the in-place upgrade.

---

## Releases process (internal note)

Releases are published automatically by GitHub Actions from the private
monorepo whenever a `v*.*.*` tag is pushed. The build runs on
`windows-latest`, produces an unsigned MSI, and uses a PAT (`RELEASES_PAT`)
to attach it to a new GitHub Release here. See the private repo's
`.github/workflows/release-tauri.yml` for the full pipeline definition.

To cut a release:

1. Bump the version in the three Tauri manifests (`tauri-app/package.json`,
   `tauri-app/src-tauri/Cargo.toml`, `tauri-app/src-tauri/tauri.conf.json`).
2. Merge a PR with the bump.
3. `git tag v0.X.0 && git push --tags` from the private monorepo.
4. Wait ~5–10 min for the Windows runner to build.
5. New release appears on this page.
