---
description: 編譯與燒錄Betaflight的基本教學
---

# Betaflight

## 韌體編譯

### 0. 前置條件

作業系統為Ubuntu或Windows WSL

### 1. 構建 Betaflight 開發環境

Betaflight 是一個開源的飛控韌體，主要用於無人機和遙控飛行器。以下是構建 Betaflight 開發環境的步驟：

### 2. 複製Betaflight Github儲存庫

1. 開啟終端。
2.  執行以下命令以複製 Betaflight 儲存庫：

    ```bash
    git clone --recursive https://github.com/betaflight/betaflight.git
    ```
3.  進入代碼庫目錄：

    ```bash
    cd betaflight
    ```
4. 安裝必要工具：`sudo apt install curl`
5.  安裝 GCC 工具鏈：

    <pre class="language-bash"><code class="lang-bash"><strong>make arm_sdk_install
    </strong></code></pre>

### 3. 編譯 Betaflight 韌體

1.  執行以下命令進行代碼編譯：

    ```bash
    make <Board Name, Ex: MATEKF405AIO>
    ```

    _將_ Board Nam&#x65;_&#x66FF;換為飛控板的具體名稱。_
2.  編譯成功後會出現以下訊息

    <figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>
3.  編譯的韌體位置在betaflight/obj底下的hex檔案

    <figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

## 韌體燒錄

1.  飛控版開啟DFU模式，USB 連接到電腦。

    <figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>
2.  使用 Betaflight Configurator 燒錄編譯好的韌體。

    <figure><img src="../../.gitbook/assets/betaflight configurator燒錄教學1.png" alt=""><figcaption></figcaption></figure>


3.  Betaflight韌體位置(hex檔案)

    <figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>


4.  開始燒錄Betaflight韌體

    <figure><img src="../../.gitbook/assets/betaflight configurator燒錄教學2.png" alt=""><figcaption></figcaption></figure>


5.  燒錄中

    <figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>


6.  燒錄完成

    <figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

***

## 自定義韌體編譯

**如何編譯自定義的飛控板**

1.  複製已經存在的飛控板定義，重新命名資料夾，EX:KAKUTEF4V2\_ICM42688P

    <figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>
2.  修改config.h

    <figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>


3.  開啟終端，切換到betaflight資料夾，編譯新飛控板的韌體:&#x20;

    `make KAKUTEF4V2_ICM42688P`
4.  編譯完的韌體將位於`betaflight/V4.5.0/betaflight/obj/`資料夾中

    <figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

