# AM32韌體線上更新

{% stepper %}
{% step %}
### 前期準備與硬體需求



1. 硬體準備

* 電子變速器（ESC）： 搭載支援 AM32 韌體之 MCU 的電調模組。
* 飛行控制器：搭載Ardupilot的飛行控制器
* 電池： 鋰電池或可調式直流電源供應器

> ⚠️ 安全警告： 在進行任何韌體刷寫、電調連線或參數修改前，務必拆除馬達上的所有螺旋槳（槳葉）。韌體寫入過程中若發生配置混亂，馬達可能會意外全速運轉，造成嚴重的設備損壞或人身傷害。

2. 準備AM32燒錄環境：建議使用Chrome瀏覽器開啟[https://am32.ca/](https://am32.ca/)
3. 硬體接線確認：ESC與飛控的排線已連接
4. 接上電源：將電池或電源供應器接上
5. 連線到電腦：將飛控的USB孔連接到電腦
{% endstep %}

{% step %}
### 確認Ardupilot韌體設定

開啟地面站，確認`SERVO_BLH_AUTO`參數設定為1

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>


{% endstep %}

{% step %}
### 透過飛控與網頁端連線

[https://am32.ca/](https://am32.ca/)網頁開啟後應該顯示如下畫面

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

點選右上角的Port Select，應會彈出選擇視窗，點選飛控的序列埠後，選擇連線

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

點選畫面右上角的Connect

<figure><img src="../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

連線成功後應出現以下畫面，接著點選Read讀取參數

<figure><img src="../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

讀取完成後應出現AM32的參數

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>


{% endstep %}

{% step %}
### 更新AM32韌體

點選畫面右上角的Flash Firmware，接著切換到Local選單，選擇要燒錄的AM32韌體

<figure><img src="../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

點選將要燒錄的MCU，即將燒錄的MCU將會呈現綠色，點選Start flash後就會開始燒錄。

如果按下Start flash後沒有進行燒錄，則ignore current mcu layout勾起來，某些自行修改的AM32韌體需要使用此選項才能夠燒錄

<figure><img src="../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>



進度條完成後表示AM32韌體更新完成
{% endstep %}
{% endstepper %}

