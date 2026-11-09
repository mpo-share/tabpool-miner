# Tabpool BRC command-line miner

This repository holds release files only. Download from [Releases](https://github.com/mpo-share/tabpool-miner/releases).

Supports BRC (BrowserCoin) only and mines on the CPU. Linux gets a single native program; Windows and macOS archives bundle their own runtime. There is nothing else to install. Use your public BRC address (64 hexadecimal characters), never a private key or seed phrase.

## Download

Current version: 1.0.0. Other versions are on the [Releases](https://github.com/mpo-share/tabpool-miner/releases) page.

| System | File |
| --- | --- |
| Windows x64 | [tabpool-brc-miner-1.0.0-win-x64.zip](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-win-x64.zip) |
| macOS Apple silicon (M1 or newer) | [tabpool-brc-miner-1.0.0-mac-arm64.tar.gz](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-mac-arm64.tar.gz) |
| macOS Intel | [tabpool-brc-miner-1.0.0-mac-x64.tar.gz](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-mac-x64.tar.gz) |
| Linux x64 | [tabpool-brc-miner-1.0.0-linux-x64.tar.gz](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-linux-x64.tar.gz) |
| Checksums | [SHA256SUMS.txt](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/SHA256SUMS.txt) |

From a terminal instead of the browser:

```powershell
# Windows PowerShell
Invoke-WebRequest https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-win-x64.zip -OutFile tabpool-brc-miner-1.0.0-win-x64.zip
Expand-Archive tabpool-brc-miner-1.0.0-win-x64.zip -DestinationPath .
```

```sh
# Linux (use mac-arm64 or mac-x64 on macOS)
curl -LO https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-linux-x64.tar.gz
```

## Windows x64

1. Download `tabpool-brc-miner-<version>-win-x64.zip`, right-click it and choose **Extract All**.
2. Double-click `tabpool-brc-miner.cmd` and enter your BRC payout address. It is saved to `config.json` in the same folder.
3. Press Ctrl+C to stop.

From cmd or PowerShell, in the extracted folder:

```cmd
tabpool-brc-miner.cmd --address <your BRC address>
```

## macOS (Apple silicon or Intel)

Download `mac-arm64` for M1 or newer, `mac-x64` for Intel Macs. In Terminal:

```sh
tar -xzf tabpool-brc-miner-<version>-mac-arm64.tar.gz
cd tabpool-brc-miner
./tabpool-brc-miner.sh --address <your BRC address>
```

If macOS blocks it, run `xattr -dr com.apple.quarantine tabpool-brc-miner` in the folder that holds it.

## Linux x64

```sh
tar -xzf tabpool-brc-miner-<version>-linux-x64.tar.gz
cd tabpool-brc-miner
./tabpool-brc-miner --address <your BRC address>
```

Or edit the address in `start.sh` and run `./start.sh`.

The program is statically linked and runs on any x86-64 Linux distribution.

## Options

Run with `--help` for the full list.

| Option | Description |
| --- | --- |
| `-a, --address <address>` | BRC payout address |
| `-t, --threads <count>` | Mining threads, default all logical cores |
| `--cpu-power <percent>` | CPU duty cycle per thread, 1-100, default 100 |
| `--worker <name>` | Worker name shown by the pool |
| `--pool <url>` | Use a different pool |

## config.json

Settings can also live in `config.json` next to the program (next to `tabpool-brc-miner.sh` on macOS). Command-line options override it.

```json
{
  "address": "<your BRC address>",
  "threads": 8,
  "cpuPower": 100,
  "worker": "my-pc"
}
```

`pool` is also accepted. Keep `config.json` when you update to a new version.

Status prints every 10 seconds. Each release includes `SHA256SUMS.txt`: check it with `sha256sum -c SHA256SUMS.txt --ignore-missing` on Linux or `shasum -a 256 <file>` on macOS. The Windows and macOS archives bundle Node.js; its licence is in `runtime/LICENSE`. The Linux program's third-party licences are in `THIRD-PARTY-LICENSES.txt` and also print with `--licenses`.
