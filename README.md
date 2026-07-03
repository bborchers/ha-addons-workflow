# ha-addons-workflow

Wiederverwendbare GitHub-Actions-Workflows (`workflow_call`) für die Home-Assistant-Add-on-Repositories von Bjoern Borchers:

- [ha-addons](https://github.com/bborchers/ha-addons) — zentrales Repository (wird in Home Assistant hinzugefügt)
- [ha-addons-grafana](https://github.com/bborchers/ha-addons-grafana) — Build-Repo für das Grafana-Addon

## Workflows

| Datei | Zweck |
|---|---|
| `.github/workflows/lint.yml` | Validiert eine Addon-`config.yaml` via `frenck/action-addon-linter` |
| `.github/workflows/commitlint.yml` | Prüft Commit-Messages gegen Conventional Commits |
| `.github/workflows/release-drafter.yml` | Pflegt einen Draft-Release mit automatisch berechneter nächster Version |
| `.github/workflows/build-deploy.yml` | Baut ein Addon multi-arch, pusht es nach GHCR und informiert `ha-addons` per `repository_dispatch` |

Aufruf-Beispiel aus einem Build-Repo:

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
