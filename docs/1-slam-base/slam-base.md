
## 传感器slam

### 激光雷达


### 视觉雷达

### 单目
单目有个最大的问题，就是没法确切地得到深度。这是一把双刃剑。
- 一方面，由于绝对深度未知，单目SLAM没法得到机器人运动轨迹以及地图的真实大小。因此，单目SLAM只能估计一个相对深度，在相似变换空间Sim(3)中求解，而非传统的欧氏空间SE(3)。如果我们必须要在SE(3)中求解，则需要用一些外部的手段，例如GPS、IMU等传感器，确定轨迹与地图的尺度（Scale）。
- 另一方面，单目相机无法依靠一张图像获得图像中物体离自己的相对距离。
单目SLAM要靠运动中的三角测量，来求解相机运动并估计像素的空间位置。
### 双目
相比于单目，双目相机通过多个相机之间的基线，估计空间点的位置。与单目不同的是，立体视觉既可以在运动时估计深度，亦可在静止时估计，消除了单目视觉的许多麻烦。不过，双目或多目相机配置与标定均较为复杂，其深度量程也随双目的基线与分辨率限制。通过双目图像计算像素距离，是一件非常消耗计算量的事情，现在多用FPGA来完成。
### RGBD
RGBD相机是2010年左右开始兴起的一种相机，它最大的特点是可以通过红外结构光或Time-of-Flight原理，直接测出图像中各像素离相机的距离。因此，它比传统相机能够提供更丰富的信息，也不必像单目或双目那样费时费力地计算深度。目前常用的RGBD相机包括Kinect/Kinect V2、Xtion等。不过，现在多数RGBD相机还存在测量范围窄、噪声大、视野小等诸多问题。出于量程的限制，主要用于室内SLAM。
### imu

-基本框架 。四个模块（除去传感器数据读取）：VO、后端、建图、回环检测。这里我们简要介绍各模块的涵义，之后再详细介绍其使用方法。

![slam-框架](https://github.com/lsy563193/image/raw/master/slam-kuangjia.jpg)


参考
[1](https://www.leiphone.com/news/201609/iAe3f8qmRHXavgSl.html)