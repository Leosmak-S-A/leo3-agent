# leo3-agent

Fleet heartbeat daemon for Leo3 industrial Raspberry Pi 5 devices (Leosmak S.A.).

Runs as a snap daemon, checking in to the Leosmak admin panel every 5 minutes to report hardware and software status.

## What it reports

| Field | Source |
|---|---|
| `serial` | `/proc/cpuinfo` Serial, or set manually |
| `fw_ver` | This snap's version (`SNAP_VERSION`) |
| `hmi_ver` | `snap list leo-control-3` (the Qt HMI snap) |
| `cpu` | `/proc/cpuinfo` Model |
| `ram` | `/proc/meminfo` MemTotal |
| `os` | `uname -r` |
| `ip` | `hostname -I` first address |

## Install

```bash
sudo snap install leo3-agent --devmode
```

## Configure per device (run once after install)

```bash
sudo snap set leo3-agent serial=LEO3-009
sudo snap set leo3-agent admin-url=http://192.168.0.10:2105
sudo snap restart leo3-agent
```

## Admin panel

Data visible at: **CI/CD → Leo3 Machines**  
API endpoint: `POST /api/v2/Leosmak/admin//tasks/leo3_checkin`

## Build

Built and published automatically by TeamCity (`Leo3Agent_Build` config).
