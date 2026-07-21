---
description: AM32韌體參數
---

# AM32參數

<figure><img src="../../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

## 馬達基礎設定 (Motor)

### 可開關

* 堵轉保護 / 失速保護 (Stuck Rotor / Stall Protection)：
  * 作用： 當馬達被異物卡住或失去遙控訊號時，電調會自動斷電或降速，防止馬達燒毀。
* 30 毫秒遙測 (30 ms Telemetry)：
  * 作用： 回傳角度、溫度等數據的頻率，透過TX線回傳基於KISS協議的封包，如果有使用AM32 TX線作為電機遙測可以使用。
* 使用霍爾傳感器 (Use Hall Sensors)：
  * 作用： 針對有感無刷馬達使用，目前已被AM32官方棄用。若馬達沒有感應線，請保持關閉。
* 互補 PWM (Complementary PWM)：
  * 作用： 在 PWM 關閉期間，將 PWM 應用於互補輸出。開啟後會產生制動效果並產生大量熱能，通常建議關閉
* PWM類型：AM32如何控制PWM
  * Fixed：選一個固定的 PWM 頻率（例如 24 kHz、48 kHz），整個轉速範圍都用同一個開關頻率
  * Variable：Variable 模式是「隨著 commutation 頻率（也就是 RPM 提升）同步提高 PWM 頻率」，目標是讓每個換相週期內的 PWM 脈衝數量保持大致一致，從低速到高速維持近乎線性的輸出。**一班來說建議開啟這個**
  * by RPM：讓 PWM 頻率與馬達轉速相關，但邏輯比較偏向「依 RPM 區間切換 PWM 頻率」，而不是完全連續地隨換相頻率線性拉動。

### 可調數值

* 電機進角 (Timing Advance)：
  * 作用： 讓馬達換向的時間比中性點提前指定的角度。
  * 影響： 高進角可以減少失步現象，但更耗電且馬達易過熱。
* 啟動功率 (Startup Power)：
  * 作用： 設定馬達啟動時允許的最大功率。負載較大（槳葉重）時可調高，預設值 115 約對應 $$3S$$ 電池。
* 電機 KV (Motor KV)：
  * 作用： 每升高 $$1V$$ 電壓，馬達增加的理論轉速。此設定需盡可能貼近馬達實際數值，電調會依此計算保護閾值。
  * 特性： 低 KV 馬達扭力大；高 KV 馬達轉速高。
* 電機磁極數 (Motor Poles)：
  * 作用： 轉子磁鐵的數量。電調利用此數值計算實際轉速，並在異常（過低或過高轉速）時觸發功率保護。
* 提示音量 (Beep Volume)：
  * 作用： 設定馬達發出嗶嗶聲的大小。
* PWM 頻率 (PWM Frequency)：
  * 作用： MOSFET 開關的頻率。頻率越高，馬達控制精度更高，但是對MCU負擔越大。

***

## 轉向設定

<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

* Reversed：馬達反轉
* 3D mode：「正反雙向旋轉、油門中立居中」的雙向推力模式，本質上就是 Betaflight/BLHeli32 用語裡的 3D / bidirectional mode。
