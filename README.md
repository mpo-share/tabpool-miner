# Tabpool BRC command-line miner

Mine BRC (BrowserCoin) on your CPU with the Tabpool pool, without keeping a browser open. Nothing else needs to be installed.

> **Use your public BRC address only.** It is 64 characters of `0-9` and `a-f`, with no `0x` in front. Never type a private key or seed phrase into this program or anywhere else.

## 1. Pick your download

Not sure which one? Use the first file that matches your computer.

| Your computer | Download this |
| --- | --- |
| Windows 10 / 11 | [tabpool-brc-miner-1.0.0-win-x64-native.zip](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-win-x64-native.zip) |
| Mac with Apple M1, M2, M3 or newer | [tabpool-brc-miner-1.0.0-mac-arm64.tar.gz](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-mac-arm64.tar.gz) |
| Mac with an Intel processor | [tabpool-brc-miner-1.0.0-mac-x64.tar.gz](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-mac-x64.tar.gz) |
| Linux (x86-64 PC or server) | [tabpool-brc-miner-1.0.0-linux-x64.tar.gz](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-linux-x64.tar.gz) |
| Windows, if your antivirus blocks the file above (see [Antivirus warnings](#antivirus-warnings)) | [tabpool-brc-miner-1.0.0-win-x64.zip](https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-win-x64.zip) |

Which Mac do I have? Apple menu → **About This Mac**. "Chip: Apple M…" means Apple silicon; "Processor: Intel" means Intel.

Older versions and `SHA256SUMS.txt` are on the [Releases](https://github.com/mpo-share/tabpool-miner/releases) page.

## 2. Start mining

### Windows

1. Find the downloaded `.zip` in your Downloads folder.
2. **Right-click it → Extract All → Extract.** Do not run anything from inside the zip without extracting: the miner cannot save your address there, and Windows may block it.
3. Open the extracted `tabpool-brc-miner` folder and double-click **`tabpool-brc-miner.exe`**.
   - If Windows shows "Windows protected your PC", click **More info → Run anyway**.
4. A black window asks for your BRC payout address. Paste it (right-click pastes in that window) and press Enter.
5. Mining starts. Leave the window open. To stop, press **Ctrl+C** or close the window.

Next time, just double-click `tabpool-brc-miner.exe` again. Your address is remembered in `config.json` in the same folder.

### macOS

Open **Terminal** (Applications → Utilities) and run these lines. On an Intel Mac, use `mac-x64` instead of `mac-arm64`:

```sh
cd ~/Downloads
tar -xzf tabpool-brc-miner-1.0.0-mac-arm64.tar.gz
cd tabpool-brc-miner
xattr -dr com.apple.quarantine .
./tabpool-brc-miner.sh
```

Paste your BRC address when asked and press Enter. Press **Ctrl+C** to stop. Next time, run `./tabpool-brc-miner.sh` from the same folder.

The `xattr` line stops macOS from blocking a program downloaded from the internet. You only need it once.

### Linux

```sh
curl -LO https://github.com/mpo-share/tabpool-miner/releases/download/brc-v1.0.0/tabpool-brc-miner-1.0.0-linux-x64.tar.gz
tar -xzf tabpool-brc-miner-1.0.0-linux-x64.tar.gz
cd tabpool-brc-miner
./tabpool-brc-miner
```

Paste your BRC address when asked. Press **Ctrl+C** to stop.

On a server without a keyboard, give the address on the command line (`./tabpool-brc-miner --address <your BRC address>`), or edit `start.sh` (replace `YOUR_BRC_ADDRESS`) and run `./start.sh`. To keep mining after you log out, run it inside `screen` or `tmux`, or with `nohup ./start.sh > miner.log 2>&1 &`.

The program is statically linked and runs on any x86-64 distribution. It does not run on ARM boards such as a Raspberry Pi.

## 3. Check that it works

Within a minute you should see lines like these:

```text
[12:00:02] Logged in, waiting for work...
[12:00:02] New job at height 98376
[12:00:12] 2.85 kH/s (avg 2.10 kH/s) | accepted 9 | stale 0 | rejected 0 | blocks 0
```

- **kH/s** is your speed. The first status line can be low or 0 while the miner warms up.
- **accepted** should go up over time. That is the work the pool credits to your address.
- A few **stale** shares are normal (the block changed while you were working on it). Many **rejected** shares are not: see [Troubleshooting](#troubleshooting).

## Settings

The easiest way to change settings is to edit `config.json` in the miner folder with Notepad or any text editor. It is created the first time you enter your address.

```json
{
  "address": "your 64-character BRC address",
  "threads": 8,
  "cpuPower": 100,
  "worker": "my-pc"
}
```

| Setting | Command-line option | What it does |
| --- | --- | --- |
| `address` | `-a`, `--address` | Where your rewards go. Required. |
| `threads` | `-t`, `--threads` | How many CPU threads to use. Default: all. Use fewer to keep the computer responsive. |
| `cpuPower` | `--cpu-power` | 1–100. Lower it (for example 50) to run cooler and quieter. Default 100. |
| `worker` | `--worker` | A name for this computer on the pool, so you can tell several machines apart. Letters, digits, `.`, `_`, `-`, up to 32 characters. |
| `pool` | `--pool` | Leave this out unless you were told to use a different pool. |

Command-line options win over `config.json`, for example `tabpool-brc-miner.exe --threads 4`. Run with `--help` to list every option.

- **Wrong address?** Open `config.json` and fix it, or delete `config.json` and start the miner again to be asked afresh.
- **Computer feels slow while mining?** Set `threads` to about half your CPU threads, or lower `cpuPower`.
- **Updating to a new version?** Extract the new download, then copy your old `config.json` into the new folder.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| The window opens and closes immediately (Windows) | Make sure you extracted the zip first. If it still closes, click the folder's address bar, type `cmd`, press Enter, then run `tabpool-brc-miner.exe` there to read the error. |
| "A BRC address is 64 hexadecimal characters" | You pasted something else. Check for a `0x` prefix, spaces, or a missing character. Use the public address from your BRC wallet. |
| "... is not valid JSON" | `config.json` has a typo. Text values need double quotes, numbers do not, and items are separated by commas. Or delete the file and start again. |
| Stuck at "Connecting" or "Connection lost" | Check your internet connection. The miner retries every 5 seconds on its own. A company or school network may block it. |
| Speed stays at 0 H/s | Wait for "New job at height …". If it never appears, restart the miner. |
| "Permission denied" (macOS / Linux) | Make sure you are inside the `tabpool-brc-miner` folder and extracted it with the `tar` command above; some archive tools drop the permission to run. |
| "cannot execute binary file" (Linux) | Your machine is not x86-64 (for example ARM). This build will not run there. |
| Antivirus deleted or blocked a file | See [Antivirus warnings](#antivirus-warnings). |

## Antivirus warnings

Antivirus programs and browsers flag almost every crypto miner as "CoinMiner" or "potentially unwanted", whatever its source. The Windows download is a single program, `tabpool-brc-miner.exe`, that is not code-signed, so your browser may refuse to download it or Windows Defender may delete it.

If that happens, either add an exclusion for the miner folder in your antivirus, or use the **Node.js build** instead: download `tabpool-brc-miner-1.0.0-win-x64.zip`, extract it, and double-click `tabpool-brc-miner.cmd`. It runs the same miner with the official, signed Node.js runtime (`runtime/node.exe`), which is rarely blocked, and reads the same `config.json`. It is a little slower.

You can check that your download is the published file by comparing its SHA-256 with `SHA256SUMS.txt` on the Releases page: `certutil -hashfile <file> SHA256` on Windows, `shasum -a 256 <file>` on macOS, `sha256sum <file>` on Linux.

## Licences

The Windows and Linux programs list their third-party licences in `THIRD-PARTY-LICENSES.txt` and print them with `--licenses`. The macOS downloads and the Windows Node.js build include Node.js; its licence is in `runtime/LICENSE`.
