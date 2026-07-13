# ❓ 常見問答 FAQ

## 組裝階段

**Q1. 接上電源後無反應、LED 不亮**\
A1. 檢查ESC輸出到飛控的線路是否正常，並確認電池無鬆脫或空焊；如果有空焊請重新補焊 XT60 並檢查電源線確保焊點良好。

**Q2. 插入 DJI O3／O4 Air Unit 後無影像或影像無飛行資訊**\
A2. 核對 TX/RX 對應；確認 Air Unit 供電12V是否正常，Serial1是否設定為DisplayPort

**Q3. GPS 無定位或衛星數過低**\
A3. 將 GPS 天線朝天、置於機體上方，盡可能不要與電池及馬達靠近；設定 GPS\_TYPE = Auto、BAUD = 115200；檢查 TX 腳持續輸出資料。

**Q4. 電機轉向錯誤**\
A4. 在Mission Planner調整SERVO\_BLH相關參數，詳細參數可參考[Ardupilot參數列表](https://ardupilot.org/copter/docs/parameters.html#servo-blh-mask-blheli-channel-bitmask)

***

## 韌體燒錄與設定

**Q5. 無法進入DFU模式**\
A5. 按下飛控板上的Boot按鍵後上電進入DFU模式，用裝置管理員看是否有出現DFU裝置，如果還是沒有出現請聯絡我們。

**Q6. 燒錄後重啟無法連線**\
A6. 使用STM32 CubeProgrammer做一次全晶片清除，接著再次燒錄，如果一樣無法連線請聯絡我們。

**Q7. IMU 或 Baro 不被偵測**\
A7. 檢查I2C設備是否有地址衝突，請逐一測試每個I2C設備是否可以正常連線。

**Q8. DShot600 無輸出**\
A8. 確保 SERVO\_BLH相關參數是否已啟用，並且有SERVO\_DSHOT\_ESC有設定正確

***

## 首次飛行

**Q9. 起飛後劇烈震動、PID 失控**\
A9. 檢查機架是否足夠堅硬，並平衡螺旋槳；鎖緊機臂螺絲（1.5–2 N·m）並檢查或替換減震墊

**Q10. Loiter模式漂移，降落時炸機**\
A10. 起飛前等待衛星 ≥ 15 顆、HDOP ≤ 0.8；把 GPS 立桿加高 6–8 cm 並重新校正磁羅盤。

***

> 如仍無法排除，請準備 **照片／影片、黑盒 Log、韌體版本**，歡迎將問題回報到service@taiphoon.com.tw ，我們將於48小時內閱讀並盡力協助診斷。

<h2 align="center">祝您飛行順利！</h2>
