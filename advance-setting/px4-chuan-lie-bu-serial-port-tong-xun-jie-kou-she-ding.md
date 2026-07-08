---
description: 如何理解與設定PX4的接口設定
---

# PX4-串列埠(Serial Port)通訊接口設定

## 確認PX4韌體設定(PX4 Firmware Configuration)

#### 切換到PX4工作目錄

`cd PX4-Autopilot`

#### 確認PX4的STM32 UART設定

`make <編譯目標名稱> menuconfig`

這邊可以看到目前的韌體啟用的那些UART介面

<figure><img src="../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

#### 確認PX4的Serial Ports定義與設定

`make <編譯目標名稱> boardconfig`

<figure><img src="../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

選擇Serial ports，將會列出PX4可以使用的Serial Port定義，以及目前**串列埠設備**對應到的**串列埠功能**

<figure><img src="../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

實際上飛控板的UART定義與串列埠設備(/dev/ttySx)的具有對應關係，在某些飛控板設計中可能會有UART沒有全部都被使用、或是跳過部分的UART接口的現象，以Morakot為例，沒有使用到UART4接口，以下為對應關係：

**UART編號**：實際上STM32使用的UART通道

**串列埠設備名稱：**&#x50;X4使用**串列埠設備名稱**來定義串列埠(接近於Linux系統的串列埠管理方式)，不同於Ardupilot直接使用UART編號

**PX4定義的串列埠功能：**&#x5728;PX4韌體中定義了串列埠的功能，在[參數表](https://docs.px4.io/main/zh/advanced_config/parameter_reference#telemetry)中可以查到**串列埠功能編號，**&#x5F8C;續在PX4參數設定中很重要

<table><thead><tr><th width="131.571533203125">串列埠順序</th><th>UART編號</th><th>串列埠設備名稱</th><th>PX4定義的串列埠功能</th></tr></thead><tbody><tr><td>1</td><td>USART1</td><td>/dev/ttyS0</td><td>TEL1</td></tr><tr><td>2</td><td>USART2</td><td>/dev/ttyS1</td><td>TEL2</td></tr><tr><td>3</td><td>USART3</td><td>/dev/ttyS2</td><td>TEL3</td></tr><tr><td>4</td><td>UART5</td><td>/dev/ttyS3</td><td>GPS</td></tr><tr><td>5</td><td>USART6</td><td>/dev/ttyS4</td><td>TEL4</td></tr><tr><td>6</td><td>UART7</td><td>/dev/ttyS5</td><td>WIFI</td></tr><tr><td>7</td><td>UART8</td><td>/dev/ttyS6</td><td>RC</td></tr></tbody></table>

#### PX4參數設定

PX4韌體運行時會再次封裝不同通訊接口(不限於串列埠)的功能，例如

* **TEL\_FRSKY\_CONFIG：**&#x46;rSky Telemetry的串列埠接口，自帶FrSky的封包收發工具
* **TEL\_HOTT\_CONFIG：**&#x48;oTT Telemetry的串列埠接口，自帶HoTT的封包收發工具
* **MAV\_1\_CONFIG：**&#x7B2C;一個使用MAVLink的串列埠接口，自帶MAVLink的封包收發工具
* **MAV\_2\_CONFIG：**&#x7B2C;二個使用MAVLink的串列埠接口，自帶MAVLink的封包收發工具
* **MAV\_3\_CONFIG：**&#x7B2C;三個使用MAVLink的串列埠接口，自帶MAVLink的封包收發工具

<details>

<summary>使用場景1: 設定WIFI數傳(UART轉WIFI)，並使用MAVLink通訊協定</summary>

1. 確認已經定義了UART7是連接到WIFI數傳，並且在`boardconfig`中也確實定義`/dev/ttyS5`是`WIFI tty port`
2.  開啟Q Ground Control，連接到飛控後開啟參數頁面，搜尋`MAV_`



    <figure><img src="../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>
3. 觀察到有MAV\_0、MAV\_1、MAV\_2，分別為不同的MAVLink通訊埠實例，可以選擇沒有使用到的實例當作WIFI數傳的設定，在這邊以MAV\_1為例
4.  搜尋MAV\_1，點選MAV\_1\_CONFIG，將會彈出一個視窗顯示要輸入的數字



    <figure><img src="../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>
5.  數字可以在PX4參數參照表找到，找到原本韌體定義的串列埠功能，填入對應的數字，按下Save儲存



    <figure><img src="../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>
6. 飛控重新啟動後即可生效
7.  以QGC或MissionPlanner測試是否以WIFI成功連通



    <figure><img src="../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

</details>

