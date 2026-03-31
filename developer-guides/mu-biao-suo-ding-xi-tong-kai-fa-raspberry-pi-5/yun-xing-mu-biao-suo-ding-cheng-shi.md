# 運行目標鎖定程式

## 樹梅派端



### 開啟Mediamtx程式

如果沒有設定為開機後自動運行，則需手動開啟

```bash
cd /path/to/mediamtx
./mediamtx
```

### 將Mediamtx設定為開機自動運行(Optional)

#### 1. 建立 Systemd 服務檔案

首先，使用 `nano` 編輯器建立一個新的服務設定檔：

```bash
sudo nano /etc/systemd/system/mediamtx.service
```

#### 2. 貼入設定內容

在編輯器中貼入以下內容。請注意： 如果你的 `mediamtx` 執行檔或 `mediamtx.yml` 設定檔不是放在 `/usr/local/bin/` 或預設目錄，請根據實際路徑修改 `ExecStart` 與 `WorkingDirectory`。

```
[Unit]
Description=MediaMTX RTSP Server
After=network.target

[Service]
# 如果你將執行檔放在其他地方，請修改此處路徑
ExecStart=/home/taiphoon/wayne/mediamtx/mediamtx /home/taiphoon/wayne/mediamtx/mediamtx.yml
WorkingDirectory=/home/taiphoon/wayne/mediamtx
Restart=on-failure
RestartSec=5
StandardOutput=append:/var/log/mediamtx.log
StandardError=append:/var/log/mediamtx.log

[Install]
WantedBy=multi-user.target
```

***

#### 3. 載入並啟用服務

執行以下命令來重新載入系統配置，並將 MediaMTX 設定為開機自啟動：

```bash
# 重新載入 systemd 配置
sudo systemctl daemon-reload

# 設定開機自啟動
sudo systemctl enable mediamtx

# 立即啟動服務
sudo systemctl start mediamtx
```

***

#### 4. Systemctl管理指令

設定完成後，你可以透過以下指令來監控或管理 MediaMTX：

* 檢查狀態： `sudo systemctl status mediamtx`
* 停止服務： `sudo systemctl stop mediamtx`
* 重啟服務： `sudo systemctl restart mediamtx`
* 查看即時日誌： `journalctl -u mediamtx -f`

### 開啟目標鎖定程式

```
~/wayne/tracker_with_rtsp/main
```

## 地面站端

### 開啟VLC驗證功能(Optional)

開啟VLC後啟動網路串流

<figure><img src="../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

輸入串流位置並按下播放，啟動連線

<figure><img src="../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

查看畫面

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

