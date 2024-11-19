# Dementia-Gesture-Game 
## Jetson Nano 密集課程專題 - Group 10  
在這一個project中，我們訓練了一個MLP模型，用以判斷手部骨架資料，最終在jetson nano上設計出了互動式猜酒拳遊戲。  

## 目的
隨著人口老齡化加劇，預計到2050年將有1.31億人罹患失智症。研究顯示，手指運動能改善認知功能並延緩輕度認知障礙（MCI）進展為失智症。

本遊戲的目的是：

* 促進認知健康：透過手指運動刺激大腦，改善或維持老年人認知功能。
* 延緩認知退化：以遊戲方式鼓勵持續運動，可能延緩認知衰退。
* 增強社交互動：提供老年人與他人互動的平台，提升社交參與。
* 提升生活品質：讓老年人在遊戲中保持大腦和身體活躍。

## 遊戲GUI: 
![alt game](./media/game.png)

## Build project on Jetson Nano:
Python version: 3.6.9  
Jetpack version: 4.6.1  
Docker image for built envrionment: ```docker pull jim0406/nano_course:latest```, which this docker is based from https://jetson-docs.com/libraries/mediapipe/l4t32.7.1/py3.6.9

確保啟動 Docker 容器時掛載 X11 和 USB 設備:
```
docker run -it --rm \
  --device=/dev/video0:/dev/video0 \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -e DISPLAY=$DISPLAY \
  --privileged \
  my_docker_image
```
## 遊戲其他功能:
用以紀錄每次猜拳反應時長  
<img src="./media/test.png" width="30%">

## Debug:
Jetson USB device連接問題 (X11 display error): 
```
xhost +SI:localusr:root
docker restart
```
Jetson 平台上，X11 是用來管理顯示的視窗系統。
默認情況下，X11 僅允許當前用戶訪問，這會導致 Docker 容器內的應用程式（例如 GUI 應用程式）無法顯示到主機屏幕上。
該命令通過設置 X11 訪問控制列表，允許 root 用戶（Docker 容器默認用戶）使用主機的顯示設備。




