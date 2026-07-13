---
description: 首次飛行前，請確保以下項目，並根據地面站軟體的提示判斷是否異常，如果無異常表示可以準備起飛
---

# 首次飛行First Flight

請依序檢查以下事項，在檢查前請先確認

* **遙控器已開機**
* **螺旋槳未安裝**
* **電池固定牢固**
* **地面站已開機**

確認完成後，接上電池



{% stepper %}
{% step %}
### 確認與地面站連線

請確保通信模組與地面站連線完畢

<figure><img src="../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### 電池電壓

確認電池電壓在24V以上

<figure><img src="../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### GPS衛星數量

確認衛星數量至少15顆，並且hdop在0.8以下

<figure><img src="../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### 確認飛行模式

撥動飛行模式桿位，依序設定為Stabilize、AltHold、Loiter(以Ardupilot為例)


{% endstep %}

{% step %}
### 確認馬達鎖

為了確保安全，應在遙控器上設置一個馬達鎖撥桿，並確認是否有效

並且將馬達鎖鎖上，HUD上應該顯示Motors Emergency Stopped

<figure><img src="../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### 裝上螺旋槳

{% hint style="warning" %}
裝上螺旋槳後，要注意遙控器被誤觸，以及地面站非必要請勿下任何操作
{% endhint %}

安裝螺旋槳時需要注意安裝方向，請依照順序擺放，並且鎖緊螺旋槳

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### 馬達測試

再次確認馬達轉向與螺旋槳安裝方向，打開馬達測試介面，並**解開遙控器上的馬達鎖**，依序以10%油門測試四顆馬達，確認**風向都是向下吹**

<figure><img src="../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### 準備起飛

切換成Stabilize模式，地面站觀察員應注意以下資訊

1. 是否有錯誤訊息或異常訊息在HUD上面?
2. Vibe與EKF是否異常

<figure><img src="../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

如果有任何異常訊息應停止起飛，並解決問題後直到儀表板顯示Ready to Arm才能解鎖
{% endstep %}

{% step %}
### 解鎖起飛

遙控器左邊桿位打置右下解鎖，並逐步加大油門讓飛機離地，觀察是否有異音或異常擺動，請試圖維持在空中1分鐘。

完成後即可降落。
{% endstep %}

{% step %}
### 飛行參數調整

首次飛行使用的參數為預設參數，因此參數一定會需要調整，請根據調參指南進行進一步調整
{% endstep %}
{% endstepper %}



