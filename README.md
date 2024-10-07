# slam_viewer

![C++](https://img.shields.io/badge/c++-17std-blue)
![Ubuntu](https://img.shields.io/badge/platform-ubuntu20.04-orange)
![build](https://img.shields.io/badge/build-pass-green)

# 1.介绍



基于pangolin，提供常规的slam可视化api，具体的使用示例可参考examples文件夹下的相关内容。使用slam_viewer非常方便，代码涉及到的流程主要有：

1. WindowImpl创建；
2. View创建（Menu菜单、Plotter数据绘图、3d可视化View3D和ImageShower四种）；
3. Camera创建并绑定View3D；
4. WindowImpl绑定View；
5. 动态创建UIItem并绑定到View3D中。

在使用样例中有针对KITTI-Odometry数据集的可视化操作，涉及到的渲染UI主要有 Trajectory（轨迹）、Frame（视觉SLAM帧）、Coordinate（坐标系）、Cloud（点云）、Image（图像）。除此之外，还有Menu菜单的配置，主要针对相机的操作，提供了跟踪模式，上帝视角和前置模式三部分的示例。

除此之外，slam_viewer为拓展留了一些常用的接口，如：
1. CloudUI部分的颜色工厂，用户可以方便的自定义一些可视化的颜色；
2. UIItem的3d渲染基类，用户可以自定义一些3d渲染的UIItem；
3. Menu菜单部分的配置，可以通过Menu内置api和lambda表达式的方式快速配置。

# 2.依赖
1. C++17
2. [OpenCV 3.4.16](https://github.com/opencv/opencv/releases/tag/3.4.16)
3. [Pangolin 0.9.1](https://github.com/stevenlovegrove/Pangolin/releases/tag/v0.9.1)
4. Eigen3
5. PCL
6. TBB

针对opencv和pangolin需要去指定的github仓库下载源码进行源码编译和安装。而Eigen3、PCL和TBB则直接通过apt进行安装。
```shell
sudo apt install libeigen3-dev libpcl-dev libtbb-dev
```

# 3. 编译

```shell
git clone https://github.com/sunshanlu/slam_viewer.git
cd slam_viewer
```

1.编译实例程序
```shell
cmake .. -DBUILD_EXAMPLES=ON -DCMAKE_BUILD_TYPE=Release
make -j8
```

2.不编译实例程序
```shell
cmake .. -DBUILD_EXAMPLES=OFF -DCMAKE_BUILD_TYPE=Release
make -j8
```

# 4. 使用示例
具体的使用示例请看examples文件夹，若要运行`kitti_dataset_example`示例，需要下载`kitti-odometry`数据集，并且需要将数据集按照如下目录存放
```shell
.
├── results
│   ├── 00.txt
│   ├── 01.txt
│   ├── xx.txt
├── sequences
│   ├── 00
│   │   ├── image_0
│   │   │   │   ├── 000000.png
│   │   │   │   ├── 000001.png  
│   │   │   │   ├── xxx.png  
│   │   └── image_1
│   │   │   │   ├── 000000.png
│   │   │   │   ├── 000001.png  
│   │   │   │   ├── xxx.png  
│   │   └── times.txt
│   ├── ...
└── velodyne
    └── sequences
        ├── 00
        │   └── velodyne
        │       ├── 000000.bin
        │       ├── 000001.bin
        │       ├── xxx.bin
        ├── ...
```

运行`kitti_dataset_example`的命令如下：
```shell
./bin/kitti_viewer <dataset_path> <sequence>
```
1. data_path: 数据集路径，也就是上述目录中的.对应的绝对路径
2. seqcuece: 00/01/...，代表kitti数据集序列
