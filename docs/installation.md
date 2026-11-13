# Install VeloTrak from the GitHub Release

VeloTrak v1.0.0 is distributed as a Linux binary on [GitHub Releases](https://github.com/VeloTrak/Velotrak/releases/tag/v1.0.0). The binary is the tracker. PostgreSQL and ClickHouse are separate, and the official installer sets them up for you.

These notes match the v1.0.0 release assets and the installer at https://velotrak.app/install.sh as published on 13 Nov 2026. The release notes on that tag are the short version of the same steps.

## What the release contains

| Asset | Role |
| --- | --- |
| `velotrak-linux-amd64` | Statically linked ELF for Linux x86_64. 18,055,352 bytes. |
| `velotrak-linux-arm64` | Statically linked ELF for Linux arm64 / aarch64. 17,301,688 bytes. |
| `checksums.txt` | SHA-256 of both binaries. |
| `manifest.json` | Version `1.0.0`, plus the URL, size, and SHA-256 of each binary. |

There is no Windows or macOS build, no Docker image of the tracker, and no source tree in this repository. `file` reports the amd64 build as a stripped, statically linked ELF. The arm64 asset is the matching build for that architecture.

SHA-256 from the v1.0.0 `checksums.txt`:

```text
69e783cab882a77669fc2c396ff935df4b432d4410f864a0fd8022864ca25001  velotrak-linux-amd64
81527c10a24069c92332fd7fb8d9dc449880135893ecbacfca0aa737f63fe59d  velotrak-linux-arm64
```

Direct downloads:

- https://github.com/VeloTrak/Velotrak/releases/download/v1.0.0/velotrak-linux-amd64
- https://github.com/VeloTrak/Velotrak/releases/download/v1.0.0/velotrak-linux-arm64
- https://github.com/VeloTrak/Velotrak/releases/download/v1.0.0/checksums.txt
- https://github.com/VeloTrak/Velotrak/releases/download/v1.0.0/manifest.json

## Server requirements

| | |
| --- | --- |
| OS | Linux with systemd. The installer refuses anything else. |
| CPU | x86_64 or arm64. |
| Minimum | 2 vCPU / 4 GB RAM. The floor tier is sized for at least 800 clicks per second (about 69 million a day). The installer warns when it sees under about 3,500 MB of RAM. |
| Recommended | 4 vCPU / 8 GB. |
| Access | root, and `curl`. |
| Hosting | You rent the machine. A VPS from about $10/month runs the floor tier. VeloTrak does not sell the server. |

## Install with the official command

On a fresh Linux server, as root:

```bash
curl -fsSL https://velotrak.app/install.sh | sudo bash
```

That command, as shipped on 13 Nov 2026, does four things:

1. Downloads `velotrak-linux-amd64` or `velotrak-linux-arm64` from this GitHub repo's latest release (or from the version you pin) and checks it against `checksums.txt`.
2. Installs Docker, if it is missing, and starts PostgreSQL (`postgres:18-alpine`) and ClickHouse (`clickhouse/clickhouse-server:24.8-alpine`) with Docker Compose. Both listen on `127.0.0.1` only. Passwords are generated.
3. Writes `/opt/velotrak/velotrak.env` (database DSNs and a generated master key) and a systemd unit named `velotrak`.
4. Starts the service and waits until `http://127.0.0.1:8080/healthz` answers.

VeloTrak itself is the native binary at `/opt/velotrak/velotrak`, not a container.

Then open:

```text
http://<this-server>:8080/admin/
```

Create the admin account there. If the page does not load from your browser, open TCP port 8080 on the firewall or cloud security group.

Useful paths after a default install:

| Path or URL | What it is |
| --- | --- |
| `/opt/velotrak/velotrak` | The binary |
| `/opt/velotrak/velotrak.env` | Config. Restart with `systemctl restart velotrak` after you edit it. |
| `/opt/velotrak/stack` | Docker Compose stack for the bundled databases |
| `/var/lib/velotrak` | Data directory, including the GeoIP database the installer tries to download |
| `http://127.0.0.1:8080/healthz` | Local health check |
| `journalctl -u velotrak -f` | Logs |

The env file the installer writes sets `VELOTRAK_HTTP_PORT` (8080), `VELOTRAK_ADMIN_PATH` (`admin`), `VELOTRAK_DATA_DIR`, `VELOTRAK_PG_DSN`, `VELOTRAK_CH_DSN`, and `VELOTRAK_MASTER_KEY`. Commented lines are there for TLS, either an ACME domain or certificate files.

## Pin v1.0.0, or install a binary you already verified

Pin the release:

```bash
curl -fsSL https://velotrak.app/install.sh | sudo VELOTRAK_VERSION=v1.0.0 bash
```

Or download the asset, check it, and hand that file to the installer:

```bash
curl -fL -o velotrak-linux-amd64 https://github.com/VeloTrak/Velotrak/releases/download/v1.0.0/velotrak-linux-amd64
curl -fL -o checksums.txt https://github.com/VeloTrak/Velotrak/releases/download/v1.0.0/checksums.txt
sha256sum -c checksums.txt --ignore-missing
curl -fsSL -o install.sh https://velotrak.app/install.sh
sudo bash install.sh ./velotrak-linux-amd64
```

On arm64, use `velotrak-linux-arm64` instead. The release notes also document `sha256sum -c checksums.txt --ignore-missing`; the installer runs that check itself when it downloads the asset.

`VELOTRAK_DOWNLOAD_BASE` can point at a mirror that serves the same file names as the release.

## Bring your own PostgreSQL and ClickHouse

```bash
curl -fsSL https://velotrak.app/install.sh | sudo VELOTRAK_EXTERNAL_DB=1 bash
```

The installer skips Docker, writes placeholder DSNs in `/opt/velotrak/velotrak.env`, and stops so you can edit them. Then:

```bash
systemctl start velotrak
```

Migrations are built into the binary. You can also run them yourself once both DSNs are set:

```bash
velotrak migrate
```

## What the binary does on its own

These commands were checked against the v1.0.0 amd64 binary:

| Command | Behavior |
| --- | --- |
| `velotrak version` or `velotrak --version` | Prints `velotrak 1.0.0 linux/amd64 license-root=production`. No database required. |
| `velotrak` | Starts the server. It needs PostgreSQL. With no env file it tries `user=velotrak`, database `velotrak`, on `127.0.0.1:5432`. |
| `velotrak migrate` | Applies built-in migrations. Requires `VELOTRAK_PG_DSN` and `VELOTRAK_CH_DSN`. |
| `velotrak activate <license key>` | Activates a license. Requires `VELOTRAK_PG_DSN`. |
| `velotrak license` | License command. Requires `VELOTRAK_PG_DSN`. |

Running the binary by hand still requires PostgreSQL and ClickHouse. The installer is the path the release documents for a first boot.

## Upgrade

Run the install command again. The env file, passwords, and data are left in place. The previous binary is kept as `/opt/velotrak/velotrak.old`. A licensed install can also update from the admin panel.

## After the service is up

The in-app wizard is five steps: timezone and currency, a traffic source (30+ templates), a campaign and flow (25 condition fields), then CAPI for Meta, TikTok, and Google. Free includes one CAPI account per platform.

To confirm the version that is actually running:

```bash
/opt/velotrak/velotrak version
```

## Uninstall notes

The installer does not ship an uninstall command. Stopping the product is `systemctl disable --now velotrak`. The databases it created live in the Docker Compose project under `/opt/velotrak/stack`. Export or back up before you delete `/opt/velotrak` or `/var/lib/velotrak`. Your click data is only on that server.
