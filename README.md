# ha-addons-workflow

Reusable GitHub Actions workflows (`workflow_call`) for Bjoern Borchers's Home Assistant add-on repositories:

- [ha-addons](https://github.com/bborchers/ha-addons) — central repository (added to Home Assistant)
- [ha-addons-grafana](https://github.com/bborchers/ha-addons-grafana) — build repo for the Grafana add-on

## Workflows

| File | Purpose |
|---|---|
| `.github/workflows/lint.yml` | Validates an add-on's `config.yaml` via `frenck/action-addon-linter` |
| `.github/workflows/commitlint.yml` | Checks commit messages against Conventional Commits |
| `.github/workflows/release-drafter.yml` | Maintains a draft release with an automatically computed next version |
| `.github/workflows/build-deploy.yml` | Builds an add-on multi-arch, pushes it to GHCR, and notifies `ha-addons` via `repository_dispatch` |

Example call from a build repo:

```yaml
jobs:
  deploy:
    uses: bborchers/ha-addons-workflow/.github/workflows/build-deploy.yml@main
    with:
      addon-path: grafana
      slug: grafana
    secrets:
      dispatch-token: ${{ secrets.DISPATCH_TOKEN }}
    permissions:
      contents: read
      packages: write
```
