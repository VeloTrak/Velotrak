# Changelog

Release notes for the binaries on [GitHub Releases](https://github.com/VeloTrak/Velotrak/releases). This repository does not contain the application source.

## 1.0.0 — 2026-11-13

First published release: [v1.0.0](https://github.com/VeloTrak/Velotrak/releases/tag/v1.0.0).

Assets:

- `velotrak-linux-amd64`
- `velotrak-linux-arm64`
- `checksums.txt`
- `manifest.json`

### Install

On a fresh Linux server (x86_64 or arm64), as root:

```bash
curl -fsSL https://velotrak.app/install.sh | sudo bash
```

Installs VeloTrak with PostgreSQL and ClickHouse (Docker is installed if missing), starts it as a systemd service and prints the admin URL. Minimum 2 vCPU / 4 GB RAM; recommended 4 vCPU / 8 GB.

### Upgrade

Run the same command again; configuration and data are kept. Licensed installs also update themselves from the admin panel.

### Verify

`sha256sum -c checksums.txt --ignore-missing` — the installer does this automatically.

Docs and pricing: https://velotrak.app
