# ❓ 常見問答 FAQ

## 組裝階段

**Q1. 接上電源後無反應、LED 不亮**\
A1. 檢查 5 V／VBAT 輸出是否正常；確認電池電壓 ≥ 11 V；重新補焊 XT60 或電源線並確保焊點良好。

**Q2. 插入 DJI O3／O4 Air Unit 後無影像**\
A2. 核對 TX/RX 對應；確認 Air Unit 供電選擇 9 V；改用較短或屏蔽線並降低雜訊。

**Q3. GPS 無定位或衛星數過低**\
A3. 將 GPS 天線朝天、置於機體上方；設定 GPS\_TYPE = Auto、BAUD = 115200；檢查 TX 腳持續輸出資料。

**Q4. 電機轉向錯誤或亂跳**\
A4. 在 BLHeli Configurator 調整 Spin Direction；確認螺旋槳正反向與 Betaflight Motor Tab 排列一致。

***

## 韌體燒錄與設定

**Q5. 無法進入 DFU／STM32Boot 模式**\
A5. 短接 BOOT0→3.3 V 後上電；更換四芯 USB 資料線；安裝 STM32 或 Zadig 驅動。

**Q6. Betaflight 韌體下載卡在 50 % 或壓縮錯誤**\
A6. 清除瀏覽器快取後重新下載；或改用無痕模式／CLI 啟動參數。

**Q7. 燒錄後重啟無法連線**\
A7. 在 CLI 輸入 `version` 確認 Target 為 **TAIPHOON\_F7**；若錯誤，使用含 bootloader 的 .hex 重新燒錄。

**Q8. IMU 或 Baro 不被偵測**\
A8. 在 `resource` 檢查感測器掛載的 SPI/I²C 匯流排；若擴充裝置地址衝突，修改原始碼並重新編譯。

**Q9. DShot600 無輸出**\
A9. 確保 `MOTOR_PWM_PROTOCOL = DSHOT600`、`DMA_OPTION = 1`，並避免同腳位啟用 LED\_STRIP／Buzzer／OSD。

***

## 首次飛行

**Q10. 起飛後劇烈震動、PID 失控**\
A10. 更換並平衡螺旋槳；鎖緊機臂螺絲（1.5–2 N·m）；檢查或替換減震墊並調低 Gyro LPF。

**Q11. 電機啸叫或動力中斷**\
A11. 監看 ESC 溫度，> 80 °C 時降低 PWM 頻率或加散熱；更換高 C-Rating 新電池以減少瞬降。

**Q12. Failsafe 無預警觸發**\
A12. 保持 Rx 與 VTX 距離 ≥ 3 cm；確保 RSSI > 40 dB，必要時使用信號放大器或 Crossfire。

**Q13. DJI OSD 文字閃爍或缺字**\
A13. 減少一次顯示項 (`CONFIG_OSD_PROFILES = 2`)；將對應 UART 鮑率設為 115200。

**Q14. GPS Hold 漂移 > 5 m，降落時炸機**\
A14. 起飛前等待衛星 ≥ 15 顆、HDOP ≤ 1.2；把 GPS 立桿加高 6–8 cm 並重新校正磁羅盤。

***

> 如仍無法排除，請準備 **照片／影片、黑盒 Log、韌體版本**，歡迎將問題回報到service@taiphoon.com.tw ，我們將於48小時內閱讀並盡力協助診斷。

<h2 align="center">祝您飛行順利！</h2>
