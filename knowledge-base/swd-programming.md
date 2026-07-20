# SWD燒錄

### 什麼是 SWD <a href="#swd" id="swd"></a>

SWD（Serial Wire Debug）是 ARM 微控制器常用的兩線式除錯與燒錄介面，可用來直接對 MCU 進行韌體寫入、記憶體存取、除錯與恢復操作。

對飛控產品而言，SWD 的最大價值在於它工作在硬體層級，即使板上的 Bootloader 或主韌體已經損壞，仍然有機會透過 SWD 重新寫入並救回板子。

### 為什麼飛行控制器會需要 SWD <a href="#morakot--swd" id="morakot--swd"></a>

在飛行控制器使用過程中，多數使用者會透過 USB 與地面站進行韌體安裝，不需要直接用到 SWD。

但在以下情況，SWD 會是必要工具：

* 第一次燒錄 Bootloader。
* 韌體或 Bootloader 損壞，板子無法正常透過 USB 啟動時。
* 進行飛行控制器開發、客製化韌體或底層除錯時。
* DFU 模式無法正常使用，需直接對 MCU 寫入映像檔時。

### SWD 的基本訊號 <a href="#swd" id="swd"></a>

SWD 最核心的訊號只有兩條，再加上一條共地線即可建立基本連線。

| 訊號    | 名稱                   | 方向        | 用途           |
| ----- | -------------------- | --------- | ------------ |
| SWDIO | Serial Wire Data I/O | 雙向        | 傳輸資料與控制命令。   |
| SWCLK | Serial Wire Clock    | 燒錄器 → MCU | 提供 SWD 通訊時脈。 |
| GND   | Ground               | -         | 共地參考。        |

實務上，很多飛控除錯接口還會另外引出 3.3V、UART TX、UART RX、nRST 或 SWO，以便同時進行供電檢測、除錯輸出或重置控制。

### SWD 如何工作 <a href="#swd" id="swd"></a>

SWD 的燒錄器會直接連到 MCU 內部的除錯埠，因此可以在不依賴主韌體正常運作的情況下，直接讀寫 Flash、暫存器與部分周邊狀態。

這也是 SWD 與一般 USB 韌體升級最大的差異。USB 更新通常需要板子至少能進入 Bootloader 或 DFU；但 SWD 是在更底層的層級與晶片溝通，所以特別適合救援與開發用途。

### 何時應該使用 SWD <a href="#swd" id="swd"></a>

建議把 SWD 視為「底層維修與開發介面」，而不是日常操作方式。

適合使用 SWD 的情境包括：

1. 新板首次寫入 Bootloader。
2. 誤刷錯誤韌體，導致板子無法啟動。
3. USB 無法辨識、DFU 失效，需直接恢復 Flash 內容。
4. 需要驗證板級接線、啟動流程或進行單步除錯。

### 一般韌體更新與 SWD 的差異 <a href="#swd" id="swd"></a>

一般韌體更新通常會透過 Mission Planner、QGroundControl 或 STM32CubeProgrammer 的 USB/DFU 模式完成

SWD 與一般方式可簡單區分如下：

| 方式        | 適用情境                        | 是否適合日常更新 |
| --------- | --------------------------- | -------- |
| USB 地面站燒錄 | 一般韌體升級、正常維護。                | 是。       |
| USB DFU   | Bootloader/韌體異常時的備援方式。      | 視情況而定。   |
| SWD       | 初次 Bootloader 燒錄、磚化救援、板級開發。 | 否。       |

### 需要準備的工具 <a href="#undefined" id="undefined"></a>

SWD 燒錄至少需要一個相容的 ST-LINK 類燒錄器；例如 ST-LINK V3 Mini，因為它除了 SWD 之外，也能透過同一個 USB 連線提供虛擬序列埠功能。

* ST-LINK V2、ST-LINK V3 Mini 或其他相容 SWD 燒錄器。
* 對應的飛控轉接線或轉接板。
* USB 線材與電腦。
* 燒錄工具，例如 STM32CubeProgrammer 或 stlink 工具鏈。

### 建議接線鏈路 <a href="#undefined" id="undefined"></a>

SWD 燒錄的連線概念可簡化為下列路徑：

`電腦 ↔ USB ↔ ST-LINK ↔ SWD 轉接線 ↔ Debug Port`

### 軟體環境 <a href="#undefined" id="undefined"></a>

* **Windows 使用者**：優先使用 STM32CubeProgrammer 進行圖形化燒錄。
* **Linux 使用者**：可使用 stlink 開源工具鏈進行燒錄與除錯。

若要處理板級開發與 Bootloader 寫入，應確認工具版本足夠新，避免裝置辨識異常。



### 常見錯誤 <a href="#undefined" id="undefined"></a>

* **接頭或轉接方式錯誤**：燒錄器接口不一定能直接插到飛控除錯口，常需要對應的轉接板或正確腳位對照。
* **Bootloader 類型錯誤**：若燒入與目標韌體堆疊不相容的 Bootloader，後續更新流程可能失敗。
* **Flash Address 錯誤**：STM32 常見 Flash 起始位址為 `0x08000000`，若寫入位址錯誤，可能表面顯示成功但板子無法啟動。
* **工具版本過舊**：舊版 stlink 工具可能無法辨識較新 MCU 或較新 ST-LINK 韌體。
* **供電衝突**：ST-LINK 可能提供 3.3V 目標電壓，但不應透過除錯口為高電流周邊供電，也需避免與外部供電形成衝突。

### 注意事項 <a href="#undefined" id="undefined"></a>

**注意：** 在接上 ST-LINK 前，請先確認 SWDIO、SWCLK 與 GND 沒有接反，且不要把高電流模組電源誤接到除錯口。

**注意：** 若板子仍可正常透過 USB 與 DFU 模式刷寫，建議優先使用既有的標準燒錄流程；只有在 Bootloader 損壞、無法開機或板級開發時，才建議使用 SWD。

### 建議操作流程 <a href="#undefined" id="undefined"></a>

1. 確認對應除錯接口。
2. 準備 ST-LINK 與轉接線。
3. 對照腳位接上 SWDIO、SWCLK、GND，必要時接 3.3V / nRST。
4. 開啟 STM32CubeProgrammer 或 stlink 工具。
5. 連線確認 MCU 可被辨識。
6. 寫入 Bootloader 或指定韌體映像。
7. 完成後重新上電，檢查 USB、Bootloader 或地面站是否可正常連線。

