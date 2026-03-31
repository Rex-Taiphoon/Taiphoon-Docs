# 範例程式碼

## 樹梅派端運行程式

主程式: video\_stream\_rtsp\_with\_tracker\_V2.cpp

```cpp
// video_stream_rtsp_with_tracker_V2.cpp

#include <opencv2/opencv.hpp>
#include <opencv2/tracking.hpp>
#include <iostream>
#include <stdio.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <fcntl.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <signal.h> // 用於處理 Ctrl+C

// 定義指令結構，增加一個 quit 標記
struct __attribute__((packed)) Command {
    int is_tracking; // 0: Unlock, 1: Lock
    int x, y, w, h;  // 追蹤框座標與大小
    int quit;        // 1: 關閉程式, 0: 繼續運行
};

// 全域變數以便信號處理
bool keep_running = true;
void signal_handler(int s) { keep_running = false; }

int main() {
    // 註冊 Ctrl+C 處理
    signal(SIGINT, signal_handler);

    // 1. 初始化 UDP Socket
    int sockfd = socket(AF_INET, SOCK_DGRAM, 0);
    struct sockaddr_in servaddr;
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = INADDR_ANY; // 本機監聽
    servaddr.sin_port = htons(14666);

    if (bind(sockfd, (const struct sockaddr *)&servaddr, sizeof(servaddr)) < 0) {
        perror("Bind failed");
        return -1;
    }

    // 設定為非阻塞
    fcntl(sockfd, F_SETFL, O_NONBLOCK);

    // 2. 開啟相機
    cv::VideoCapture cap(0);
    if (!cap.isOpened()) return -1;
    cap.set(cv::CAP_PROP_FRAME_WIDTH, 640);
    cap.set(cv::CAP_PROP_FRAME_HEIGHT, 480);
    cap.set(cv::CAP_PROP_FPS, 30);

    // 3. 設定 FFmpeg
    std::string ffmpeg_cmd = "ffmpeg -y -f rawvideo -pixel_format bgr24 -video_size 640x480 -i - "
                             "-c:v libx264 -preset ultrafast -tune zerolatency -g 30 "
                             "-f rtsp -rtsp_transport tcp rtsp://localhost:8554/wayne_video0 -loglevel quiet";
    FILE* pipe = popen(ffmpeg_cmd.c_str(), "w");

    cv::Mat frame;
    cv::Ptr<cv::Tracker> tracker;
    bool is_locked = false;
    cv::Rect roi;
    Command cmd = {0, 0, 0, 0, 0, 0};

    std::cout << "系統啟動，等待指令於 Port 14666..." << std::endl;

    while (keep_running && cap.read(frame)) {
        // --- A. 接收與過濾 UDP 指令 ---
        struct sockaddr_in cliaddr;
        socklen_t len = sizeof(cliaddr);
        Command incoming;
        
        // 嘗試讀取並獲取來源 IP
        if (recvfrom(sockfd, &incoming, sizeof(incoming), 0, (struct sockaddr *)&cliaddr, &len) > 0) {
            char* sender_ip = inet_ntoa(cliaddr.sin_addr);
            
            // 僅接受特定 IP 指令
            if (strcmp(sender_ip, "192.168.6.220") == 0) {
                printf("Receive command from %s!!\n", sender_ip);
                
                // 檢查是否為關閉指令
                if (incoming.quit == 1) {
                    keep_running = false;
                    break;
                }

                if (incoming.is_tracking == 1) {
                    is_locked = true;
                    roi = cv::Rect(incoming.x, incoming.y, incoming.w, incoming.h);
                    tracker = cv::TrackerKCF::create(); 
                    tracker->init(frame, roi);
                } else {
                    is_locked = false;
                    tracker.release();
                }
            }
        }

        // --- B. 追蹤與繪圖邏輯 ---
        if (is_locked && !tracker.empty()) {
            if (tracker->update(frame, roi)) {
                cv::rectangle(frame, roi, cv::Scalar(0, 255, 0), 2);
                cv::putText(frame, "STATUS: LOCK", cv::Point(10, 30),
                            cv::FONT_HERSHEY_SIMPLEX, 1, cv::Scalar(0, 0, 255), 2);
            } else {
                cv::putText(frame, "STATUS: LOST", cv::Point(10, 30),
                            cv::FONT_HERSHEY_SIMPLEX, 1, cv::Scalar(0, 0, 255), 2);
            }
        } else {
            cv::putText(frame, "STATUS: UNLOCK", cv::Point(10, 30),
                        cv::FONT_HERSHEY_SIMPLEX, 1, cv::Scalar(0, 255, 0), 2);
        }

        // 5. 推流
        fwrite(frame.data, 1, frame.total() * frame.elemSize(), pipe);

        // 如果有顯視窗才需要 waitKey，純推流可不理會
        if (cv::waitKey(1) == 27) break;
    }

    printf("\n正在關閉服務...\n");
    close(sockfd);
    if (pipe) pclose(pipe);
    cap.release();
    return 0;
}
```

CMakeLists.txt

```
cmake_minimum_required(VERSION 3.10)
project(Wayne_Tracker)

# 設定 C++ 標準
set(CMAKE_CXX_STANDARD 11)

# 尋找 OpenCV 封裝
find_package(OpenCV REQUIRED)

# 包含標頭檔路徑
include_directories(${OpenCV_INCLUDE_DIRS})

# 執行檔設定
# add_executable(main video_stream_rtsp_with_rectangles)
add_executable(main video_stream_rtsp_with_tracker_V2.cpp)

# 連結 OpenCV 程式庫
target_link_libraries(main ${OpenCV_LIBS})
```

編譯程式

```
cmake .
```

```
make
```

## 地面軟體運行程式

發送指令的最小實作方式(Python)

```
import socket
import struct

# 指令內容: is_tracking, x, y, w, h
data = struct.pack("iiiii", 1, 50, 150, 100, 100)
sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
sock.sendto(data, ("192.168.6.222", 14666)) # 樹梅派的 IP 地址和端口號
```

