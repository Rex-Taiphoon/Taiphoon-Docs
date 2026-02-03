---
description: 以Mission Planner為主要設定工具，設定韌體為Ardupilot 4.6.3
---

# 首次設定First Setup

首次設定時，必須配置與校正一些硬體配件以及參數，並依據以下順序執行：

{% stepper %}
{% step %}
### 選擇框架類型與馬達布局(Frame Class and Type)

#### 框架結構 (Frame Class)

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

這指飛機整體的「**物理形狀**」。最常見的包括：

* Copter (多旋翼): 四軸 (Quad)、六軸 (Hexa)、八軸 (Octa)等。
* Heli: 傳統單旋翼直升機。
* Plane: 定翼機。
* Sub: 水下無人機。
* Rover: 無人車或船。

#### 馬達佈局方向 (Frame Type)

選定了框架結構後（例如 Quad），必須告訴系統**馬達的排列方向**。

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

#### 常見的四軸佈局

* X 模式: 飛行方向朝向兩隻手臂的中間。這是目前的主流，因為相機鏡頭比較不容易拍到螺旋槳，且飛行動態最對稱。
* H 模式: 雖然結構像 H，但在 ArduPilot 中通常也設定為 X 模式，除非馬達的扭矩分布有顯著物理差異。
{% endstep %}

{% step %}
### 加速度計校準(Accel Calibration)


{% endstep %}

{% step %}
### 羅盤校準(Compass Calibration)


{% endstep %}

{% step %}
### 遙控器校準(Radio Calibration)


{% endstep %}

{% step %}
### 伺服機輸出(Servo Output)

控制PWM輸出通道與功能
{% endstep %}

{% step %}
### 馬達編排、轉向與測試

#### 基礎硬體要求

1. 必須支援 BLHeli\_S、BLHeli\_32 或 AM32

#### **關鍵參數設定**

<table><thead><tr><th width="192">參數名稱</th><th width="143">設定值</th><th>說明</th></tr></thead><tbody><tr><td>MOT_PWM_TYPE</td><td>6</td><td>設定為 DShot600 (若電變較舊可選 4=DShot300)</td></tr><tr><td>SERVO_BLH_AUTO</td><td>3</td><td>自動啟用對應腳位的 BLHeli 支援</td></tr><tr><td>SERVO_DSHOT_ESC</td><td>1</td><td>啟用 DShot 遙測或進階功能</td></tr></tbody></table>

#### **馬達測試**

{% hint style="warning" %}
**注意!為了安全起見，測試前務必將螺旋槳卸下!**
{% endhint %}

常見的馬達布局為X型，正確的馬達轉向如下：

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

#### **進入馬達測試頁面**

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

馬達測試時，參數預設為Throttle=5%、Duration=2 sec。依序從馬達A開始測試到馬達D，可參照上方馬達布局圖片

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

正常來說，轉動的順序應該如下表(假設機首對向前方)：

| 按下按鍵         | 轉動馬達位置     | 轉動方向     |
| ------------ | ---------- | -------- |
| Test motor A | 右前方(馬達編號1) | 逆時針(CCW) |
| Test motor B | 右後方(馬達編號4) | 順時針(CW)  |
| Test motor C | 左後方(馬達編號2) | 逆時針(CCW) |
| Test motor D | 左前方(馬達編號3) | 順時針(CW)  |

#### **馬達編排錯誤調整方式**

如果旋轉的位置錯誤，則需要到Servo output頁面更改馬達順序

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

**假設原本的編排為如下**

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

如果按下Test motor A時，原本應為**右前方(馬達編號1)旋轉**，卻是**右後方(馬達編號4)旋轉**，表示**Motor1的功能被錯誤分配到Channel/Position 1(實體電路的PWM輸出，表示實際上的Position1不是第一顆馬達)**，因此需要把**Channel/Position 1**分別改成**Motor2\~Motor4，**&#x4E26;且**不要有MotorN設定相同**避免無法排&#x67E5;**，**&#x76F4;到測試到馬達編排順序正確。

#### **馬達轉向錯誤調整方式**

到**配置/調試介面的Full Parameters**，更改SERVO\_BLH\_RVMASK，變更完重新啟動才會生效

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

如果Motor1轉向錯誤，則需要到Servo output看Motor1對應的是哪一個**Channel/Position，**&#x4E26;將對應的**Channel/Position**勾起來，並寫入參數。以下圖為例，需要把**Channel1勾起來。**

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>


{% endstep %}

{% step %}
### 電子變速器校正(ESC Calibration)


{% endstep %}

{% step %}
### 串行接口設定(Serial Port)


{% endstep %}

{% step %}
### 飛行模式設定(Flight Mode)


{% endstep %}

{% step %}
### 故障保護設定(Failsafe)


{% endstep %}
{% endstepper %}



除了強制校準外，還可以選擇配置周邊硬體設備，包括但不限於：

1. 電池監視器(Battery Monitor)
2. 聲納(Sonar Range)
3. 空速計(Airspeed sensor)
4. 光流(Optical flow)
5. OSD
6. 相機雲台(Gimbal Camera)

***

#### 此教學所示範的系統與接線如下：

*



#### 以下將會示範Betaflight、Ardupilot、PX4韌體的首次設定

{% tabs %}
{% tab title="Betaflight" %}
*
{% endtab %}

{% tab title="Ardupilot" %}

{% endtab %}

{% tab title="PX4" %}



{% endtab %}
{% endtabs %}
