# Homework5
## Motion Parallax

### Input images:

|||
| ------------- | ------------- |
| ![](./images/img1.jpg)  | ![](./images/img2.jpg)  |

### Method:

1. Inputs為一左一右距離相近方向一致的圖片
2. 使用ORB找到features和matches之後，只留下距離最近的matches
3. 找homography，做perspective transformation，將兩張圖align在一起

![](./align1.jpg)

### Result: 

![](./output1.gif)

## Stop Motion

### Input images:

|||||
|-|-|-|-|
|![](./images/img3_1.jpg)|![](./images/img3_2.jpg)|![](./images/img3_3.jpg)|![](./images/img3_4.jpg)|
|![](./images/img3_5.jpg)|![](./images/img3_6.jpg)|![](./images/img3_7.jpg)|![](./images/img3_8.jpg)|

### Method:

1. 拍一連串連續圖片作為inputs
2. 手動框出目標物品
3. 使用ORB找到features和matches
4. 去掉背景的matches，僅留下目標物品上的matches
5. 算出rigid transformation並套用
6. 使用這次算出的圖片與下一張進行以上3~5步

![](./align2.jpg)

### Result: 

![](./output2.gif)

### Discussion: 

找出目標物品並只使用目標物品上的matches進行transform是很重要的。通常的情況下，背景的matches站大多數，因此會根據背景旋轉，造成目標移出範圍。 

![](./output2_building.gif)
