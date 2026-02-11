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

{% hint style="warning" %}
先將飛機放置在**水平的平面**上
{% endhint %}

1. 到**初始配置的Accel Calibration**介面，點選**校正加速度計**
2. 按照指示操作，依序按下**Click when Done**
3.  飛機放置水平

    <figure><img src="../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>
4.  飛機正面朝向左側(向左轉90度)

    <figure><img src="../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>
5. 依序進行校正
6.  校正完成後將出現**Finish**

    <figure><img src="../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>


7. 將飛機放置在水平面，按下**校準水平狀態**
8. ![](<../.gitbook/assets/image (88).png>)


{% endstep %}

{% step %}
### 羅盤校準(Compass Calibration)

到**初始配置的羅盤校準**介面，點選**Start**

<figure><img src="../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

校正中，直到100%即完成校正

<figure><img src="../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

完成後**重新啟動(Reboot)**
{% endstep %}

{% step %}
### 遙控器校準(Radio Calibration)

{% hint style="warning" %}
請確認已經卸下螺旋槳
{% endhint %}

#### 校正前準備

1. ✅ 遙控器已開機
2. ✅ 接收機已與遙控器對頻（Bind）
3. ✅ 飛控已正確連接接收機（SBUS / PPM / PWM）
4. ✅ 電池已接上（部分飛控需供電才會讀取接收機）
5. ✅ 油門桿在最低位置（安全）

#### 開始校正

1. 進入Radio Calibration介面
2. 按下開始校準
3. 撥動遙控器上面的每一隻撥桿，並且都要撥到最低位置與最高位置
4. 按下結束
5. 結束遙控器校準
{% endstep %}

{% step %}
### 伺服機輸出(Servo Output)

到**初始配置的Servo Output**介面

<figure><img src="../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

可以在對應的**通道/位置**選擇不同的觸發功能，常見的多旋翼通道1\~4為馬達輸出通道
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

ArduPilot 提供了一種同時校正所有電調的方法，操作如下

#### 第一階段：進入校正模式

1. **開啟遙控器**，並將**油門推至最高 (100%)**。
2. 接上電池。飛控上的 LED 會以紅、藍、黃循環閃爍（代表它偵測到開機時油門在高位，準備進入校正模式）
3. 拔掉電池
4. 再次接上電池

#### 第二階段：執行校正

1. 按下安全開關 (Safety Switch)（如果你的硬體有配備，長按至紅燈恆亮）。
2. 此時ESC會發出幾聲特殊的嗶聲（通常是兩聲短音），代表它已經記錄了最大油門位置。
3. 將遙控器**油門拉至最低 (0%)**。
4. 電調會發出一聲長鳴或連續嗶聲（代表已記錄最小油門，並完成初始化）。
5. 此時**輕輕推動油門**，馬達應該會開始同步轉動。
{% endstep %}

{% step %}
### 串行接口設定(Serial Port)

到**初始配置的Serial Ports**介面

<figure><img src="../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

可以參考Morakot Flight Controller的接口映射表，根據需求調整通訊速度(Baudrate)與通訊協定(Protocol)

調整完需要**重新啟動(Reboot)**
{% endstep %}

{% step %}
### 飛行模式設定(Flight Mode)

到**初始配置的飛行模式設定**介面

<figure><img src="../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

**綠色底為目前所在的飛行模式**

1. 可以先選定遙控器上的飛行模式切換通道(桿位/按鍵)，觀察**不同狀態所在的飛行模式選項**(例如某遙控器撥桿的低桿位為飛行模式1，中桿位為飛行模式4、高桿位為飛行模式6)
2. 根據需求與習慣調整不同桿位的**飛行模式選項**
{% endstep %}

{% step %}
### 電源模組設定(Battery Monitor)

#### 校正電源模組

到**初始配置的電源模組**配置以下參數

<figure><img src="../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

1. 量測目前電池的實際電壓
2. 輸入到**量測電池電壓**欄位，確認後按下Enter
3. 量測目前電流
4. 輸入到**量測電流**欄位，確認後按下Enter

#### 校正電源模組(直接調整參數)

到**配置/調試介面的Full Parameters**介面，確認以下參數，如果使用**Morakot 4 in 1 ESC**則能夠套用以下設定值

<table><thead><tr><th width="183">參數名稱</th><th>使用Morakot 4 in 1 ESC的設定值</th><th>說明</th></tr></thead><tbody><tr><td>BATT_MONITOR</td><td>4</td><td>監控電池的電壓和電流的功能</td></tr><tr><td>BATT_CURR_PIN</td><td>12</td><td>監測電流的腳位</td></tr><tr><td>BATT_VOLT_PIN</td><td>10</td><td>監測電壓的腳位</td></tr><tr><td>BATT_AMP_PERVLT</td><td>40</td><td>電流感測器的比例換算關係</td></tr><tr><td>BATT_VOLT_MULT</td><td>11.07</td><td>電壓分壓係數</td></tr><tr><td>BATT_AMP_OFFSET</td><td>0.032</td><td>電流感測器的偏移量</td></tr></tbody></table>




{% endstep %}

{% step %}
### 故障保護設定(Failsafe)

到**初始配置的失控保護**介面，故障保護為當發生異常情況時，讓飛控自動執行預設的安全動作。

<figure><img src="../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

介面中可以選擇**三種故障保護措施與條件**

#### 1. 電池故障保護 (Battery Fail-safe)

* 電壓低於 `BATT_LOW_VOLT` 或消耗容量超過 `BATT_LOW_MAH`。
* 常見動作： RTL (返航) 或 Land (就地降落)。

#### 2. 遙控器斷訊保護 (Radio Control Fail-safe)

* 飛控連續幾百毫秒收不到遙控器信號（通常透過監測第 3 通道 PWM 值是否低於 `FS_THR_VALUE`）。
* 常見動作： 如果有 GPS 則執行 RTL；若無 GPS 則執行 Land。

#### 3. 地面站斷訊保護 (GCS Fail-safe)

* 使用數傳（Telemetry）飛行時，飛控與地面站失去連線。
* 常見動作： 通常用於自動航點任務（Auto Mission）中，決定要繼續執行任務還是立即返航。
{% endstep %}
{% endstepper %}

