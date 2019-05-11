# Homework5
## Motion Parallax

### Method:

Input為一左一右距離相近方向一致的圖片，使用ORB找到features和matches之後，只留下距離最近的matches。接下來找homography，做perspective transformation之後，將兩張圖align在一起。

### Input images:

|||
| ------------- | ------------- |
| ![](./images/img1.jpg)  | ![](./images/img2.jpg)  |

### Match: 

![](./align1.jpg)

### Result: 

![](./output1.gif)
