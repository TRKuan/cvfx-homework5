# Homework5

這次[作業](https://colab.research.google.com/drive/1eCAsc8LUDAHe0ygrlkDQYvlpuiXYCja7#scrollTo=ShRCKVL342pW)內容為使用multi-view images製照3D的特效，詳細程式見`homework5.ipynb`。

## Motion Parallax

### Input images:

|||
| ------------- | ------------- |
| ![](./images/img1.jpg)  | ![](./images/img2.jpg)  |

### Method:

1. Inputs為一左一右距離相近方向一致的圖片
2. 使用ORB找到features和matches之後，只留下距離最近的matches
3. 找homography，做perspective transformation，將兩張圖align在一起
4. Crop中間80%減少黑色邊框並輸出gif動畫

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
2. 手動框出目標物
3. 使用ORB找到features和matches
4. 去掉背景的matches，僅留下目標物上的matches
5. 算出rigid transformation並套用
6. 使用這次算出的圖片與下一張進行以上3~5步
7. Crop中間80%減少黑色邊框並輸出gif動畫

![](./align2.jpg)

### Result: 

![](./output2.gif)

### Discussion: 

#### 限制Matches在目標物上

找出目標物並只使用目標物上的matches進行transform是很重要的。通常的情況下，背景的matches站大多數，因此會根據背景旋轉，造成目標移出範圍。所用的圖片雖然很接近stereo但實際上還是有差，直接套用opencv算stereo深度會失敗。手動限縮matches範圍為簡單且能讓穩定性有一定程度提升的辦法，但仍然容易在多張圖之後出錯。

![](./output2_building.gif)

但如果背景較為單純，則不限縮matches的範圍也是可以的。如下圖:

![](./output2_cup.gif)

#### 使用Rigid Transformation

這裡使用rigid transformation而非perspective transformation的原因，是因為perspective transformation會將圖片變形，改變圖片所在的平面，使一開始的正面仍然是正面，而不會有我們想要的鏡頭移動的效果。下圖為使用perspective transformation的結果:

![](./output2_perspective.gif)

## Live Photo

### Input images:

|||||
|-|-|-|-|
|![](./images/0.JPG)|![](./images/1.JPG)|![](./images/2.JPG)|
|![](./images/3.JPG)|![](./images/4.JPG)|![](./images/5.JPG)|

### Method
我們是以洗手槽當背景，拍照時利用手搖晃裝水的馬克杯造成水面的動態效果。使用六張照片並且利用sift對第一張照片extract features和align。但因為拍照時的手以及拿馬克杯的手有些許移動，導致其與背景有相對移動，因此align出來的結果沒有很理想，但因為背景是白色為主還算是有一致，但有些微扭曲到碗的形狀。

### Result:

![](./live.gif)

## Conclusion

拍攝良好的input圖片是非常重要的，由於feature matching對於移動造成的變形並不是很robust，每個圖片之間要夠接近才能穩定且持續地找到正確的matches。而由於硬體與技術上的不足，也會造成雖然兩圖實際距離不遠，但拍出的圖片相似性很低
