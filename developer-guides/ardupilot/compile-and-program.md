---
description: 編譯與燒錄Ardupilot的基本教學
---

# Ardupilot

## 韌體編譯

### 0. 前置條件

作業系統為Ubuntu或Windows WSL

### 1. 構建 Ardupilot 開發環境

Ardupilot是一個開源的飛控韌體，主要用於無人機和遙控飛行器。以下是構建 Ardupilot開發環境的步驟：

### 2. 複製Ardupilot Github儲存庫

1. 開啟終端。
2.  執行以下命令以複製 Ardupilot 儲存庫：

    ```bash
    git clone --recurse-submodules https://github.com/ArduPilot/ardupilot.git
    ```
3.  進入儲存庫目錄：

    ```bash
    cd ardupilot
    ```
4.  執行Ardupilot開發環境配置腳本，等待安裝完成：

    <pre class="language-bash"><code class="lang-bash"><strong>Tools/environment_install/install-prereqs-ubuntu.sh -y
    </strong></code></pre>



    <figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>
5.  重新讀取路徑：

    ```
    . ~/.profile
    ```
6. 登出後再登入以儲存設定

### 3. 編譯 Ardupilot 韌體

1.  先將工作目錄切換到Ardupilot儲存庫中

    <pre><code><strong>cd ardupilot
    </strong></code></pre>
2.  執行以下命令進行韌體編譯：

    <pre class="language-bash"><code class="lang-bash"><strong>./waf configure --board &#x3C;Board Name, Ex: MATEKF405AIO>
    </strong></code></pre>

    _將_ Board Nam&#x65;_&#x66FF;換為飛控板的具體名稱。_

    <figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

    <pre><code><strong>./waf copter # 如果要編譯的是arducopter
    </strong></code></pre>


3.  編譯成功後會出現以下訊息

    <figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>
4.  編譯的韌體位置在build/\<Board Name>/bin底下，包含僅含Ardupilot韌體檔案(ardupilot.bin, ardupilot.apj)與包含bootloader的Ardupilot韌體檔案(ardupilot\_with\_bl.hex)

    <figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

## 韌體燒錄

燒錄Ardupilot韌體目前提供兩種方法

{% tabs %}
{% tab title="Mission Planner" %}
**此方法應用於已安裝PX4或Ardupilot的韌體**



1. 飛控板使用USB連接到電腦。
2.  開啟Mission Planner，開啟初始配置，**注意**不需要按下連線

    <figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>
3.  按下想要燒錄的韌體(例如Copter)，按下Yes

    <figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>
4.  燒錄中

    <figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>
5.  燒錄完成

    <figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>
6.  按下右上角連線，回到飛行數據，有姿態以及飛行數據表示燒錄完成

    <figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="STM32CubeProgrammer " %}
**此方法可以應用於原先安裝Betaflight或其他非PX4與Ardupilot的韌體**



1. 先下載並安裝STM32CubeProgrammer，[下載來源](https://www.st.com/en/development-tools/stm32cubeprog.html)
2. 飛控板開啟DFU模式，USB 連接到電腦。
3.  開啟STM32CubeProgrammer，選擇USB並按下Connect，連線到飛控板

    <figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>
4.  按下Open file，開啟包含bootloader的檔案

    <figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>
5.  下載/燒錄韌體到飛控板上

    <figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>
6.  燒錄中

    <figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>
7. 完成下載/燒錄
8.  燒錄完成

    <figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>


9.  開啟Mission Planner，連線到飛控

    <figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="QGroundControl" %}

{% endtab %}
{% endtabs %}





***

## 如何編譯自定義的飛控板

1. 確認已經成功配置Ardupilot開發環境
2.  移動到ardupilot/library/AP\_HAL\_ChibiOS/hwdef中，複製**已經存在**的飛控板定義，重新命名新飛控板名稱的資料夾，此處以Morakot為例。

    <figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>
3.  修改hwdef.dat(不含Bootloader的版本)與hwdef-bl.dat(含Bootloader的版本)

    <figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
4.  修改其中的內容，根據實際板子所使用的腳位定義與接線，撰寫自己的飛控板配置

    <figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>
5. 修改完畢後，開啟終端機，切換到ardupilot儲存庫的資料夾
6.  首先，編譯新飛控板的Bootloader，**此步驟不可跳過**。：

    `./Tools/scripts/build_bootloaders.py <Board Name>`

    <figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>
7.  接著配置Ardupilot韌體編譯設定，此時還不會編譯，**此步驟不可跳過。**

    `./waf configure --board <Board Name>`

    <figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>
8.  接著編譯Ardupilot韌體，**此步驟不可跳過。**

    `./waf copter`

    <figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>
9.  編譯完成的Ardupilot韌體將會位於ardupilot/build/\<Board Name>/bin裡面

    <figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

