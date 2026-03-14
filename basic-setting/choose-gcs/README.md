# 選擇地面控制站GCS



## 概要

地面站通常是一套執行於電腦、手機或遙控器上的軟體，透過 **無線數傳模組** 或 **USB 連線** 與無人機（UAV）溝通。它能顯示飛行時的即時資料與位置，形同「虛擬駕駛艙」，提供與真實飛機座艙類似的儀表資訊。GCS 亦可在飛行途中上傳新任務、修改參數，並常用於監看即時影像串流。\
在正式飛行前，您還需要 GCS 來設定自動駕駛 (Autopilot) 的參數與更新韌體。

目前至少有十種以上的 GCS 可供選擇，以下舉幾個較常用的GCS：

* **桌機版**：Mission Planner、MAVProxy、QGroundControl
* **行動裝置版**：QGroundControl

挑選時，可依 **使用情境** 與 **常用平台** 作考量：

* **成品機/玩家：**&#x53EF;能偏好 QGroundControl 或其他行動裝置 GCS，攜帶方便、操作直覺。
* **DIY/套件玩家與開發者：**&#x9700;要深入的設定與分析功能，初期通常必須使用 Mission Planner、QGroundControl等完整功能的桌機版 GCS。
* **程式開發者：**&#x82E5;想要可擴充的指令列介面，MAVProxy 會是好選擇。

***

#### Mission Planner

* **特色**：功能最完整、使用者數量最多
* **支援平台**：Windows、Mac OS、Linux
* **授權**：GPLv3 開源
* **資源**：[下載](https://firmware.ardupilot.org/Tools/MissionPlanner/)、[原始碼](https://github.com/ArduPilot/MissionPlanner)

#### MAVProxy

* **特色**：Linux 指令列 GCS，模組化，可用 Python 擴充
* **支援平台**：Linux
* **授權**：GPLv3 開源
* **資源**：[Wiki](https://ardupilot.org/mavproxy/)

#### QGroundControl

* **特色**：唯一同時支援桌機與行動裝置的 GCS
* **支援平台**：Windows、Mac OS、Linux、Android、iOS
* **授權**：GPLv3 開源
* **資源**：[官方網站](https://qgroundcontrol.com/)

