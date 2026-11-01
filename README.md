# Tabpool ARG command-line miner

This repository holds release files only. Download the miner from [Releases](https://github.com/mpo-share/tabpool-miner/releases).

The miner supports ARG (Argonmine) only and needs a GPU.

## Windows x64

1. Download `tabpool-miner-<version>-win-x64.zip` and extract it. Keep the `runtime` folder next to `tabpool-miner.cmd`.
2. Double-click `tabpool-miner.cmd` and enter your ARG payout address. It is remembered for next time.
3. Press Ctrl+C to stop.

You can also start it from cmd:

```cmd
tabpool-miner.cmd --address arg1...
```

Requires the [Microsoft Visual C++ Redistributable](https://aka.ms/vs/17/release/vc_redist.x64.exe).

The first run takes a few minutes to tune the lane count before the hashrate settles.

If the hashrate is low, close other programs that use VRAM. The browser ARG miner page keeps its VRAM even after you press stop, so close that tab as well.

## Linux x64 (experimental)

The Linux build has run on an RTX 3090 with NVIDIA driver 580. Other GPUs and drivers have not been tested yet.

```sh
tar -xzf tabpool-miner-<version>-linux-x64.tar.gz
cd tabpool-miner
./tabpool-miner.sh --address arg1...
```

Requires glibc 2.34 and GCC 12 libstdc++ (Ubuntu 22.04, Debian 12 or newer), plus a Vulkan loader and driver:

```sh
sudo apt install libvulkan1 mesa-vulkan-drivers
```

On NVIDIA, use the proprietary driver and skip `mesa-vulkan-drivers`.

Check the `GPU:` line after starting. `llvmpipe` means CPU emulation with a very low hashrate, so install a GPU driver.

## Options

Run with `--help` for the full list.

| Option | Description |
| --- | --- |
| `-a, --address <address>` | ARG payout address |
| `--worker <name>` | Worker name shown by the pool |
| `--gpu-power <percent>` | GPU duty cycle, default 100 |
| `--lanes <count>` | Fixed lane count that skips auto-tuning; each lane uses 8 MiB of VRAM |
| `--pool <url>` | Use a different pool |

## Verifying downloads

Each release includes `SHA256SUMS.txt`:

```sh
sha256sum -c SHA256SUMS.txt --ignore-missing
```

Antivirus software or SmartScreen may warn about this program because it is a miner. Only run files downloaded from this repository.

Third-party licences are in `runtime/licenses` after extracting.
