---
description: >-
  Morakot 4 in 1 ESC
  是專為高性能無人機應用打造的電調系統，整合四路高電流電子調速器於單一模組中，提供更高的功率密度與更簡潔的安裝方式。此設計不僅節省飛行器的空間與重量，更確保在極端環境下的穩定輸出，適合專業級與工業級無人機應用。
---

# Morakot 4 in 1 ESC

<figure><img src="../.gitbook/assets/Morakot 4 in 1 ESC(無標示).jpg" alt=""><figcaption></figcaption></figure>

## **規格** Specifications

* 輸入電壓：11V\~33.6V(3S\~8S)
* 最大電流：60A
* 預設韌體：AM32 Firmware
* 支援通訊協定：PWM、DShot300、DShot600
* 尺寸：44.3(L)\*45.7(W)\*7.55mm(H)
* 安裝孔距：30.5 x 30.5mm

<figure><img src="../.gitbook/assets/Morakot 4 in 1 ESC(有標示).jpg" alt=""><figcaption></figcaption></figure>



## **連接器接腳分配 Connectors Pin A**ssignments

**Output Connector(JST-GH 8p)**

| Pin | Signal  | Voltage     |
| --- | ------- | ----------- |
| 1   | VCC     | +12V\~33.6V |
| 2   | TX      | +3.3V       |
| 3   | GND     |             |
| 4   | CURRENT |             |
| 5   | Motor1  |             |
| 6   | Motor2  |             |
| 7   | Motor3  |             |
| 8   | Motor4  |             |

## **電源模組設定 Battery Monitor Setting**

```
// Ardupilot設定方式
BATT_MONITOR, 4 // 設定成讀取類比訊號(電壓+電流)
BATT_VOLT_MULT, 1.111838 // 設定電壓腳位每單位電壓(V)對應的實際電壓(V)
BATT_AMP_PERVLT, 30.3 // 設定電流腳位每單位電壓(V)對應到的電流(A)
BATT_AMP_OFFSET, 0.392 // 設定電流腳位在0A時的電壓(V)
```
