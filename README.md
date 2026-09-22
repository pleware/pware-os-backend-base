# pware-os-backend-base

The **base image** for the PWare OS backend (umbrella draft `73`): ubuntu 24.04
+ four apt packages + the MIT Hermes install, pinned to a reviewed commit. Built
once by CI and pulled everywhere — a box never re-runs the Hermes installer, it
`docker pull`s this layer.

This repo is **public on purpose** (73, decided 2026-09-23): it holds nothing
PWare-owned. The actual PWare code lives in the private `pware-os-cli` repo,
whose thin `Dockerfile` only does `FROM ghcr.io/pleware/pware-os-backend-base:<commit>`.

## Files

- `Dockerfile.base` — the heavy layer. Bump `HERMES_COMMIT` to a verified commit
  on a deliberate upgrade; the image tag follows.
- `.github/workflows/publish-base.yml` — builds and pushes
  `ghcr.io/pleware/pware-os-backend-base:<commit>` on a `v*` tag push.

## Publish

Tag a release (`v*`) or run the workflow manually. The image is pushed as
`ghcr.io/pleware/pware-os-backend-base:<commit>`. The commit is read from
`Dockerfile.base` itself, so the tag can never drift from the pin.

Visibility is a one-time, irreversible manual step in the package UI (GitHub has
no API for it — `cli/cli#6820`); once public, later pushes stay public.
