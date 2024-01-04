# 室内定位RFID

RFID 室内定位方法：LANDMARC算法和 VIRE 算法

##### 

## 1.测距定位算法

（1）AOA算法

AOA（Angle of Arrival）信号到达角度定位算法，就是通过待定位目标节点 O 发射的信号分别被接收机 A、B 接收到的角度为a 和 b ，然后通过接收角度a和b方位线的交点来确定未知目标节点 O 的坐标。

<img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20210909185556170.png" alt="image-20210909185556170" style="zoom: 67%;" />

<img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20210915093650779.png" alt="image-20210915093650779" style="zoom:50%;" />



（2）TOA算法

测的发射点 A、B、C 到目标 O 的到达时间分别为 T1、T2以及 T3，那么定位目标到发射点的距离可以根据公式 R=VT 获得，但是由于精度问题和传输损失可能会有所偏差，TOA 定位精度较高，关键是获得准确的 TOA 测量值，需要严格要求所有的收发机设备之间必须保持精确的时钟同步和较快的设备处理速度，因此对硬件要求较高，从而导致系统成本比较昂贵。在室内定位系统中，由于节点间的距离较小，电磁波在空气中传播速度比较快，使得传播时间较短，测距难度大，因此 TOA方法不适合空间狭小、环境复杂的室内定位

<img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20210915093902696.png" alt="image-20210915093902696" style="zoom: 40%;" />

<img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20210915094233726.png" alt="image-20210915094233726" style="zoom:50%;" />



（3）TDOA算法

与（2）相比，通过测量每两个发射器之间的差值，从而降低了误差，利用双曲线的性质，通过联立方程组的方式得到待测点的坐标。

<img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20210915094619079.png" alt="image-20210915094619079" style="zoom:50%;" />

<img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20210915094654284.png" alt="image-20210915094654284" style="zoom:67%;" />

TDOA 方法与 TOA 方法相比，严格降低了设备之间时间的精确同步，采用相对的时间差来确定待定位目标的估计位置。非视距和多径问题对电磁波的传播影响较大，对信号的到达时间差需要做精确的记录，提高了设备的复杂性和成本，同样不适合应用于区域狭小、环境复杂的室内定位

（4）RSSI 定位算法

通过模型将信号强度转化为距离，RSSI 方法系统成本低，容易搭建，但是室内环境比较复杂，存在多径、反射、
障碍物等因素的干扰，因此定位精度不稳定。

（5）指纹定位法

就是通过在阅读器范围内设置大量的参考标签，将每个参考标签的RSSI值记录到库中，就相当于指纹库，当检测目标标签RSSI值时将其与库中进行比对

## 2 定位中常用基础算法

##### （1）聚类算法

**KNN算法 （分类回归有监督）**：选取k个近邻求取加权平均作为替代

**Kmeans算法（聚类无监督）**：无监督将数据分为k类，随机选出k个中心，将所有数据与该中心求出最小距离的即归为这个类，然后我们迭代更新类中心，重复至类中心不再变化。[【机器学习】K-means（非常详细） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/78798251)

**模糊聚类算法fuzzy c-means (FCM)**：[(24条消息) FCM模糊聚类算法_HUXINY的博客-CSDN博客_fcm是什么意思](https://blog.csdn.net/HUXINY/article/details/90607216)

##### （2）贝叶斯算法

##### （3）

## 3 定位经典算法

##### （1）LANMARC算法

##### （2）VIRE算法

VIRE: Active RFID-based Localization Using Virtual Reference Elimination

为了减少LANDMARC标签放置所带来的多径干扰，在每个参考标签之间加入虚拟标签，虚拟标签RSSI值为插值平均后的值。我们把整个地方化为几个区域，每个区域的RSSI值为中心点虚拟标签的值。每个阅读器都对应一个近似图，近似图的货的过程如下，在我们得到目标标签RSSI值后，我们取一个阈值，将区域与目标标签RSSI值之差小于该阈值的区域高亮，最后我们将k个阅读器对应的k个近似图取交集。

<img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20211122214817410.png" alt="image-20211122214817410" style="zoom:67%;" />

利用取得的近似图对目标位置进行预测，我们这里对于每个区域设置两个权重值

wi1是该区域点在每个阅读器下RSSI值与目标标签RSSI的差值除以k再除以阅读器个数乘以虚拟标签RSSI值

wi2是连接区域越多权值越大

<img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20211122214935884.png" alt="image-20211122214935884" style="zoom:50%;" /><img src="C:\Users\conan\AppData\Roaming\Typora\typora-user-images\image-20211122214951548.png" alt="image-20211122214951548" style="zoom:50%;" />

总权值是wi1✖wi2，剩下方法同LANDMARC

## 4 值得阅读的论文

## 5 论文搜索期刊

International Conference on Information Fusion

Internet of thing

trans on mobil