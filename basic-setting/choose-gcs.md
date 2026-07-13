# 選擇地面控制站GCS



## 概要

地面站通常是一套執行於電腦、手機或遙控器上的軟體，透過 **無線數傳模組** 或 **USB 連線** 與無人機（UAV）溝通。它能顯示飛行時的即時資料與位置，形同「虛擬駕駛艙」，提供與真實飛機座艙類似的儀表資訊。GCS 亦可在飛行途中上傳新任務、修改參數，並常用於監看即時影像串流。\
在正式飛行前，您還需要 GCS 來設定自動駕駛 (Autopilot) 的參數與更新韌體。

目前至少有十種以上的 GCS 可供選擇，以下舉幾個較常用的GCS：

* **桌機版**：Mission Planner、QGroundControl
* **行動裝置版**：QGroundControl

挑選時，可依 **使用情境** 與 **常用平台** 作考量：

* **成品機/玩家：**&#x53EF;能偏好 QGroundControl 或其他行動裝置 GCS，攜帶方便、操作直覺。
* **DIY/套件玩家與開發者：**&#x9700;要深入的設定與分析功能，初期通常必須使用 Mission Planner、QGroundControl等完整功能的桌機版 GCS。
* **程式開發者：**&#x82E5;想要可擴充的指令列介面，MAVProxy 會是好選擇。

***

#### Mission Planner

<figure><img src="../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

與 **ArduPilot** 生態系綁定最深，如果需要最極致的**參數調校**功能與強大的行業應用工具，它是不二之選。

* 運行的作業系統： 原生支援 Windows（基於 .NET 框架開發）。
* 經常搭配的開源飛控韌體： ArduPilot (ArduCopter / ArduPlane / ArduRover)。它是 ArduPilot 官方推薦且完美契合的地面站。
* 地面站核心特色：
  * 功能全面： 從基礎的搖桿校準，到複雜的 PID 調校、天線追蹤器（Antenna Tracker）設定、甚至光流感測器配置，所有你能想到的功能它都有。
  * 強大的航線規劃（Mission Planning）： 內建極為強大的測繪工具（Survey），可以自動根據相機參數、重疊率計算出最佳的測繪航線與拍照點，是地理資訊（GIS）與植保業者的最愛。
  * 內建**模擬器（SITL）**： 允許使用者在不連接實體飛控的情況下，直接在電腦上模擬飛行與測試航線邏輯。
  * 工程感十足的介面： 缺點是視覺設計較為傳統，滿滿的表格與參數，對新手來說學習曲線非常陡峭，但在老手眼中則是無可替代的「調機神器」。
* **資源**：[下載](https://firmware.ardupilot.org/Tools/MissionPlanner/)、[原始碼](https://github.com/ArduPilot/MissionPlanner)



#### QGroundControl

<figure><img src="../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

基於 Qt 框架開發的現代化地面站，主打流暢的跨平台體驗與直覺的 UI 設計，是近年來商業無人機與新創團隊最愛改裝的基底。

* 運行的作業系統： 多平台支援： Windows、macOS、Linux、Android 以及 iOS。
  * 其在平板與手機（Android/iOS）上的觸控體驗極佳，非常適合外場作業。
* 經常搭配的開源飛控韌體： PX4 Autopilot（官方指定地面站）。
  * 同時也完整支援 ArduPilot（MAVLink 協議通用）。
* 地面站核心特色：
  * 現代化且對觸控友好的 UI： 介面設計乾淨、直覺，大按鈕與動態選單非常適合在戶外使用平板電腦操控，新手的上手速度極快。
  * 高度模組化與客製化： 由於程式碼架構基於 Qt/QML，許多商業無人機公司會直接拿 QGC 的原始碼進行二次開發，換上自己的商標（White-label）與專屬功能。
  * 優秀的視訊串流整合： 對於即時數位圖傳（Video Streaming）的支援度非常好，可以輕鬆在主畫面整合低延遲的航拍畫面。
  * 設定流程引導化： 將飛控的解鎖、校準、硬體配置做成類似「安裝精靈」的引導式步驟，大幅降低了人為誤操作的機率。
* **資源**：[官方網站](https://qgroundcontrol.com/)

