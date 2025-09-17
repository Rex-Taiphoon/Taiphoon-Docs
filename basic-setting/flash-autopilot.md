---
cover: ../.gitbook/assets/taiphoon_logo2.jpg
coverY: 0
---

# 燒錄開源飛控韌體(Autopilot)

Taiphoon產品主要以三種開源飛控韌體為主：

* Betaflight
* Ardupilot
* PX4 Autopilot

接著將會介紹Betaflight、Ardupilot、PX4韌體的安裝與基本配置方式

{% tabs %}
{% tab title="Betaflight" %}
## 先前準備

* 燒錄韌體用的地面站：Betaflight Configurator 10.10.0
* 下載韌體連結：taiphoon.com.tw/firmware/morakot/lastest
* 飛控板：Morakot

## 連接到電腦

* 長按Boot按鍵並插入USB線，啟動DFU模式
* 開啟裝置管理員，出現**STM32 BOOTLOADER**

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

## 韌體燒錄

* 開啟**Betaflight Configurator**，此時右上角應出現DFU裝置名稱，按下固件燒寫工具

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

* 按下從**本地電腦加載固件**

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

* 選擇先前下載的韌體。下載韌體連結：taiphoon.com.tw/firmware/morakot/lastest，按下**開啟**

<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

* 按下**燒寫固件**

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

* 正在擦除

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

* 正在燒錄

<figure><img src="../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

* 出現 `Configurator has successfully detected and verified the board`即完成燒錄，並且**右上角出現裝置名稱**。

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

## 連線測試

* 按下**連接**，連線到飛控

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

* 連線後可能會跳出問題視窗，燒錄新飛控韌體後第一次連線會出現是正常的，由於沒有經過感測器校正的步驟，會在**首次設定First Setup**中進一步說明，目前暫時跳過。

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

* 連線成功後，顯示飛控目前姿態與狀態數值

<figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

<h2 align="center">燒錄Betaflight韌體步驟完成！接著進行<strong>首次設定First Setup！</strong></h2>
{% endtab %}

{% tab title="Ardupilot" %}


## 先前準備

* 燒錄韌體用的地面站：Mission Planner 1.3.82
* 下載韌體連結：taiphoon.com.tw/firmware/morakot/lastest



***

透過Mission Planner
{% endtab %}

{% tab title="PX4" %}
{% hint style="info" %}
請先確認PX4 Bootloader燒錄流程，示範飛控(KakuteF4-AIO V2.1)於QGC讀不到\
\
\# PX4 Firmware Bootloader參考連結：[https://docs.px4.io/main/zh/advanced\_config/bootloader\_update\_from\_betaflight.html#bootloader-firmware](https://docs.px4.io/main/zh/advanced_config/bootloader_update_from_betaflight.html#bootloader-firmware)
{% endhint %}

## 先前準備

* 燒錄韌體用的地面站：QGroundControl 5.0.0
* 下載韌體連結：taiphoon.com.tw/firmware/morakot/lastest





## 燒錄PX4 Bootloader(非必須)

## 連接到電腦

* 長按Boot按鍵並插入USB線，啟動DFU模式
* 開啟裝置管理員，出現**STM32 BOOTLOADER**

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

## 韌體燒錄

* 開啟QGroundControl，按下左上角的Icon，點選Vehicle Configuration

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

* 按下Firmware

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

* 選擇燒錄
* 正在燒錄
* 完成燒錄

## 連線測試

* 連線到裝置
* 連線狀態驗證



<h2 align="center">燒錄Betaflight韌體步驟完成！接著進行<strong>首次設定First Setup！</strong></h2>
{% endtab %}
{% endtabs %}



