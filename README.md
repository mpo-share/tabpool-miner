# Tabpool BRC command-line miner

This repository holds release files only. Download from [Releases](https://github.com/mpo-share/tabpool-miner/releases).

Supports BRC (BrowserCoin) only and mines on the CPU. Each archive bundles its own runtime, so there is nothing else to install. Use your public BRC address (64 hexadecimal characters), never a private key or seed phrase.

## Windows x64

1. Download `tabpool-brc-miner-<version>-win-x64.zip` and extract it. Keep the `runtime` and `app` folders next to `tabpool-brc-miner.cmd`.
2. Double-click `tabpool-brc-miner.cmd` and enter your BRC payout address. It is saved to `config.json` in the same folder.
3. Press Ctrl+C to stop.

From cmd or PowerShell:

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
./tabpool-brc-miner.sh --address <your BRC address>
```

Requires glibc 2.28 or newer (Ubuntu 20.04, Debian 10 or newer).

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

Settings can also live in `config.json` next to the launcher. Command-line options override it.

```json
{
  "address": "<your BRC address>",
  "threads": 8,
  "cpuPower": 100,
  "worker": "my-pc"
}
```

`pool` is also accepted. Keep `config.json` when you update to a new version.

Status prints every 10 seconds. Each release includes `SHA256SUMS.txt`: check it with `sha256sum -c SHA256SUMS.txt --ignore-missing` on Linux or `shasum -a 256 <file>` on macOS. The bundled Node.js licence is in `runtime/LICENSE`.
