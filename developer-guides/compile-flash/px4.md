---
description: 編譯與燒錄PX4的基本教學
---

# PX4

## 韌體編譯

### 0. 前置條件

作業系統為Ubuntu或Windows WSL

### 1. 構建PX4開發環境

PX4是一個開源的飛控韌體，主要用於無人機和遙控飛行器。以下是構建 PX4開發環境的步驟：

### 2. 複製PX4 Github儲存庫

1. 開啟終端。
2.  執行以下命令以複製 Betaflight 儲存庫：

    ```bash
    git clone https://github.com/PX4/PX4-Autopilot.git --recursive
    ```
3.  執行PX4開發環境配置腳本，等待安裝完成：

    <pre class="language-bash"><code class="lang-bash"><strong>bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
    </strong></code></pre>

    <figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### 3. 編譯PX4韌體

1.  先將工作目錄切換到PX4儲存庫中

    ```
    cd PX4-Autopilot
    ```
2.  執行以下命令進行韌體編譯：

    ```bash
    make <Board Name>
    ```

    _將_ Board Nam&#x65;_&#x66FF;換為飛控板的具體名稱。_

    <figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>


3.  編譯的韌體位置在PX4-Autopilot/build/\<Board Name>/底下，包含PX4的韌體檔案(\<Board Name>.bin, \<Board Name>.px4)

    <figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

## 韌體燒錄

燒錄PX4韌體目前提供兩種方法

{% tabs %}
{% tab title="QGroundControl" %}
**此方法應用於已安裝PX4或Ardupilot的韌體**



1.  開啟QGroundControl，開啟左上角的Icon，**確保目前沒有連接飛控**

    <figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>
2.  選擇Vehicle Configuration

    <figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>
3.  選擇Firmware，提示表示請插入USB

    <figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>
4.  飛控板使用USB連接到電腦，出現以下畫面，選擇PX4 Pro字串的選項。

    <figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>
5. 按下OK即可開始燒錄
6. 回到QGC連線，觀察是否有數據，有數據表示成功
{% endtab %}

{% tab title="STM32CubeProgrammer " %}
**此方法可以應用於原先安裝Betaflight或其他非PX4與Ardupilot的韌體**



1. 先下載並安裝STM32CubeProgrammer，[下載來源](https://www.st.com/en/development-tools/stm32cubeprog.html)
2. 飛控板開啟DFU模式，USB 連接到電腦。
3.  開啟STM32CubeProgrammer，選擇USB並按下Connect，連線到飛控板

    <figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>
4.  按下Open file，開啟包含px4韌體的檔案(此處以Ardupilot為例，可以選擇.px4檔案)

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
{% endtabs %}





***

## 如何編譯自定義的飛控板

1. 確認已經成功配置PX4開發環境
2.  移動到PX4-Autopilot/board中，複製**已經存在**的飛控板定義，重新命名新飛控板名稱的資料夾，此處以Morakot為例。

    <figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>
3.  修改nuttx-config資料夾中的nsh/defconfig以及bootloader/defconfig

    nsh/defconfig，修改`CONFIG_ARCH_BOARD_CUSTOM_DIR="<nuttx-config所在的路徑>"`

    <figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

    bootloader/defconfig，修改`CONFIG_ARCH_BOARD_CUSTOM_DIR="<nuttx-config所在的路徑>"`

    <figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
4.  修改飛控板資料夾內部的檔案(目前尚未測試完成)

    <figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
5.  修改飛控板資料夾其中的內容，根據實際板子所使用的腳位定義與接線，撰寫自己的飛控板配置(目前尚未測試完成)

    <figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
6. 修改完畢後，開啟終端機，切換到PX4儲存庫的資料夾
7.  首先，編譯新飛控板的Bootloader，**此步驟不可跳過**。：

    `make <Board Name>_bootloader`

    <figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>
8.  接著編譯PX4韌體，**此步驟不可跳過。**

    `make <Board Name>_default`

    <figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
9.  編譯完成的PX4韌體將會位於`PX4-Autopilot/build/<Board Name>_default`裡面

    <figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

