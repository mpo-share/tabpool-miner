# Tabpool ARG 命令列礦工

這個 repo 只放發佈檔，請到 [Releases](https://github.com/mpo-share/tabpool-miner/releases) 下載。只支援挖 ARG，需要 GPU。

## Windows x64

1. 下載 `tabpool-miner-<版本>-win-x64.zip` 並解壓，`runtime` 資料夾要和 `tabpool-miner.cmd` 放在一起。
2. 雙擊 `tabpool-miner.cmd`，輸入 ARG 收款地址。地址會被記住，下次不用再輸入。
3. 按 Ctrl+C 停止。

也可以從 cmd 執行：

```bat
tabpool-miner.cmd --address arg1...
```

需要安裝 [Microsoft Visual C++ 可轉散發套件](https://aka.ms/vs/17/release/vc_redist.x64.exe)。

第一次執行要等幾分鐘調整 lane 數，算力才會穩定。

算力偏低時，請先關閉其他佔用顯示記憶體的程式。瀏覽器的 ARG 礦工頁即使按了停止，仍會佔著顯示記憶體。

## Linux x64（實驗性）

Linux 版只用軟體 Vulkan 跑過完整流程，還沒在真實 GPU 上驗證。

```sh
tar -xzf tabpool-miner-<版本>-linux-x64.tar.gz
cd tabpool-miner
./tabpool-miner.sh --address arg1...
```

需要 glibc 2.34 與 GCC 12 的 libstdc++（Ubuntu 22.04、Debian 12 或更新），以及 Vulkan loader 與驅動。Ubuntu／Debian 可以這樣安裝，NVIDIA 顯示卡則改用官方驅動，不裝 `mesa-vulkan-drivers`：

```sh
sudo apt install libvulkan1 mesa-vulkan-drivers
```

啟動時請看 `GPU:` 那一行。如果顯示 `llvmpipe`，代表沒有用到顯示卡，而是用 CPU 模擬，算力會非常低，請安裝顯示卡驅動。

## 參數

執行時加上 `--help` 可以看到所有參數。

| 參數 | 用途 |
|---|---|
| `-a`, `--address <地址>` | ARG 收款地址 |
| `--worker <名稱>` | 礦池顯示的礦工名稱 |
| `--gpu-power <百分比>` | GPU 使用比例，預設 100 |
| `--lanes <數量>` | 固定 lane 數並跳過自動調整，每個 lane 佔 8 MiB 顯示記憶體 |
| `--pool <網址>` | 改連其他礦池 |

## 確認下載的檔案

每個版本都附有 `SHA256SUMS.txt`，可以用來核對檔案是否完整：

```sh
sha256sum -c SHA256SUMS.txt --ignore-missing
```

防毒軟體或 SmartScreen 可能因為這是礦工程式而發出警告，請只執行從這裡下載的檔案。

第三方元件的授權聲明在解壓後的 `runtime/licenses` 資料夾。
