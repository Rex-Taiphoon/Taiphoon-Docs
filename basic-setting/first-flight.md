# 首次飛行First Flight

首次飛行前，由於有許多參數可能尚未調整到位，因此必須做一些基本的飛行前檢查表(Preflight checklist)，包含GCS與無人系統的檢查表

***

GCS(Ground Control Station)

<table><thead><tr><th width="78">項次</th><th>檢查內容</th><th>通過標準</th></tr></thead><tbody><tr><td>1</td><td>GCS電腦</td><td>已開機(Power On)</td></tr><tr><td>2</td><td>GCS電腦電量</td><td>>50%</td></tr><tr><td>3</td><td>GCS軟體(QGC、Mission Planner)</td><td>已開啟</td></tr><tr><td>4</td><td>數傳模組</td><td>已連接</td></tr><tr><td>5</td><td>連接UAS</td><td>已連接</td></tr><tr><td>6</td><td>錯誤訊息</td><td>無錯誤訊息</td></tr><tr><td>7</td><td>安全檢查設定(Pre-Arm Safety Checks)</td><td>已設定</td></tr><tr><td>8</td><td>電池電壓</td><td>>12.5V(3S, LiPo)<br>>16.5V(4S, LiPo)<br>>20.5V(5S, LiPo)<br>>24.5V(6S, LiPo)</td></tr><tr><td>9</td><td>訊號品質</td><td>>75%</td></tr><tr><td>10</td><td>RC控制信號</td><td>控制Pitch、Roll、Yaw、Throttle軸，觀察控制信號是否變化</td></tr><tr><td>11</td><td>馬達緊急停止(Motor Emergency Stop)設定</td><td>已設定馬達緊急停止</td></tr><tr><td>12</td><td>飛行模式控制桿</td><td>撥動飛行模式控制桿確認設定正確</td></tr><tr><td>13</td><td>GPS狀態</td><td>已定位3D Fixed，衛星數>10顆</td></tr><tr><td>14</td><td>解鎖怠速(Idle)設定</td><td>確認解鎖怠速已設定</td></tr><tr><td>15</td><td>飛行模式</td><td>Betaflight: Angle Mode<br>Ardupilot: Stabilize Mode<br>PX4: Attitude Mode</td></tr></tbody></table>



***

UAS

<table><thead><tr><th width="81">項次</th><th>檢查內容</th><th>通過標準</th></tr></thead><tbody><tr><td>1</td><td>螺旋槳</td><td>安裝正確</td></tr><tr><td>2</td><td>圖傳天線(可選)</td><td>已安裝</td></tr><tr><td>3</td><td>數傳天線</td><td>已安裝</td></tr><tr><td>4</td><td>整機螺絲與配件</td><td>已鎖緊</td></tr><tr><td>5</td><td>電池組</td><td>已安裝</td></tr><tr><td>6</td><td>連接電池</td><td>已連接</td></tr><tr><td>7</td><td>飛控初始化完成</td><td>初始化完成且無異音</td></tr><tr><td>8</td><td>遙控器</td><td>油門收至最底、其他控制軸向置中</td></tr></tbody></table>

***

## 以上項目確認完成後，油門桿收至最底，航向軸(Yaw)往內收，解鎖飛機。

參考資料：

1\. [https://ardupilot.org/copter/docs/checklist.html](https://ardupilot.org/copter/docs/checklist.html)

