# Security

VeloTrak is self-hosted. Clicks, conversions, and campaign configuration stay on the operator's server. This repository publishes release binaries and documentation, not the application source.

## Reporting a vulnerability

Email [support@velotrak.app](mailto:support@velotrak.app). Please include:

- The version (`/opt/velotrak/velotrak version`, or the release tag)
- What is affected (the tracker binary, the installer at https://velotrak.app/install.sh, or this documentation)
- A short description of the impact, and a way to reproduce it if you have one

Do not file a public GitHub issue for an unfixed vulnerability. Do not send license keys, database DSNs, master keys, or exports of click and conversion data. If a screenshot is necessary, remove those values first.

## What stays on your server

The [privacy policy](https://velotrak.app/privacy/) says business data in your PostgreSQL and ClickHouse is not sent to VeloTrak. A license check-in sends an install identifier, the software version, the plan, and the license status. Telemetry is off by default. Tracking continues if licensing fails, with a 30-day offline grace period.

Operating the server, the firewall, backups, and database passwords is the operator's responsibility. The terms of service say the same thing: https://velotrak.app/terms/

## Release binaries

v1.0.0 binaries are published on [GitHub Releases](https://github.com/VeloTrak/Velotrak/releases/tag/v1.0.0) with `checksums.txt`. The official installer verifies the SHA-256 before it replaces `/opt/velotrak/velotrak`. Check a manual download with:

```bash
sha256sum -c checksums.txt --ignore-missing
```
