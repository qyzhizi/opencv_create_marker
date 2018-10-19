# opencv_create_marker
### 生成的marker
![marker](https://github.com/qyzhizi/opencv_create_marker/blob/master/out_10.jpg?raw=true)
### code explain
#### 平台
`ubuntu 16.04`
`opencv3.4.1` <br>
`contrib-3.4.1` 用到头文件：`#include <opencv2/aruco.hpp>`<br> 
#### 使用的是代码是官方例程
**注释原代码块：**<br>
这个可以不用，只要在程序中配置好参数就可以
```
    // if(argc < 4) {
    //     parser.printMessage();
    //     return 0;
    // }

```
```
namespace {
const char* about = "Create an ArUco marker image";
const char* keys  =
        "{@outfile |out_2_5_200.jpg | Output image }"//定义输出marker的名字
        "{d        |  2    | dictionary: DICT_4X4_50=0, DICT_4X4_100=1, DICT_4X4_250=2,"//选择一个特定的字典
        "DICT_4X4_1000=3, DICT_5X5_50=4, DICT_5X5_100=5, DICT_5X5_250=6, DICT_5X5_1000=7, "
        "DICT_6X6_50=8, DICT_6X6_100=9, DICT_6X6_250=10, DICT_6X6_1000=11, DICT_7X7_50=12,"
        "DICT_7X7_100=13, DICT_7X7_250=14, DICT_7X7_1000=15, DICT_ARUCO_ORIGINAL = 16}"
        "{id       |  5   | Marker id in the dictionary }"
        "{ms       | 200   | Marker size in pixels }"
        "{bb       | 1     | Number of bits in marker borders }"
        "{si       | 1 | show generated image }";
}
```
dict`DICT_4X4_100=1`：represent dict‘s content is 4x4 picture and have 100 classes

``` c++ 
    cv::Mat markerImage; cv::aruco::Dictionary dictionary = cv::aruco::getPredefinedDictionary(cv::aruco::DICT_6X6_250);

    cv::aruco::drawMarker(dictionary, 23, 200, markerImage, 1); 
```
 **drawMarker的参数如下：**

 - 第一个参数是之前创建的字典对象。
 - 第二个参数是marker的id，在这个例子中选择的是字典DICT_6X6_250第23个marker。注意到每个字典是由不同数目的Marker组成的，在这个例子中，有效的Id数字范围是0到249。不在有效区间的特定id将会产生异常。
- 第三个参数，200，是输出Marker图像的大小。在这个例子中，输出的图像将是200x200像素大小。注意到这一参数需要满足能够存储特定字典 的所有位。所以，举例而言，你不能为6x6大小的marker生成一个5x5图像（这还没有考虑到Marker的边界）。除此之外，为了避免变形，这一参数最好和位数+边界的大小成正比，至少要比marker的大小大得多（如这个例子中的200)，这样变形就不显著了。
- 第四个参数是输出的图像。
最终，最后一个参数是一个可选的参数，它指定了Marer黑色边界的大小。这一大小与位数数目成正比。例如，值为2意味着边界的宽度将会是2的倍数。默认的值为1。
生成的图像如下：
![marker](https://github.com/qyzhizi/opencv_create_marker/blob/master/out_2_5_200.jpg?raw=true)<br>
具体代码见：`create_marker.cpp`




