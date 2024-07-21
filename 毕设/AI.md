6.6

卷积神经网络的目的：：1提取丰富的特征， 2 提取关联性强的特征值

**filter卷积核** （权重），例如3x3矩阵x3对应RGB

**数据**: 图像为例，单次操作为（3x3x3矩阵），最后3表示RGB数据

**算法**：卷积核 与 数据 内积 + 权重 = 该数据组成的特征明显度， 相当于w x = y

**卷积核大小**：表示矩阵大小，越小越好，最合适的3x3

**卷积核个数**：越多越好，设置多个filter与数据卷积，得到丰富的特征

**滑动窗口步长stride**：每次移动1格

**边缘填充pad**：卷积时候，有的数据被计算多次，对结果影响较大，设置边界

**卷积层数**：下一层是对上一次的结果进行再次提取，卷积层越多，具有的宏观信息越多

**池化POOL**：对每个特征进行缩小，如 每个特征由32x32x3数据构成，池化后为10x10x3，池化只改变特征大小，不改变特征数量

**最大池化MAX POOL**：池化的方法，选取特征最大的数据，来缩小特征   



![image-20240606122446495](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406061224543.png)

**神经网络层数layers **：含有偏重的层（卷积层CONV） FC全连接层

在 YOLO（You Only Look Once）目标检测模型中，网格和边界框是关键概念，它们用来表示和检测图像中的目标。为了更通俗易懂地解释这些概念，我们可以把 YOLO 过程想象成在一幅图像上进行的“精确瞄准”的游戏。



**YOLO**

**网格（grid）** 

- **划分图像**：在 YOLO 中，我们将图像分成一个固定数量的网格。例如，如果我们把图像分成 `7x7` 的网格，那么整个图像被分成 49 个小方块（网格单元）。

- **职责分配**：每个网格单元的任务是负责检测位于该单元中心的目标。
  
  - 如果一个目标（如车、狗、或人）的中心落在某个网格单元内，这个单元就负责预测这个目标。
  
    

**边界框(bounding box)**是用来精确描述图像中目标位置的矩形框。

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202406201654646.png" alt="image-20240620165412594" style="zoom:50%;" />

- **描述目标**：每个边界框由四个关键参数组成：
  
  - **`x` 和 `y`**：目标在网格单元内的位置，通常是==边界框中心点==相对于==网格单元左上角==的偏移。
  - **`w` 和 `h`**：边界框的宽度和高度，通常是相对于整个图像的比例（例如，目标占图像宽度的 30%）。
  - **置信度**：表示该框中==是否存在目标==及其准确性（即，模型对这个框中存在目标的信心程度）。
  - **类别概率**：表示目标属于每个==类别的概率==（例如，这个框里是狗的概率 vs. 是猫的概率）。
  
- **多个预测**：在 YOLO 中，每个网格单元不只预测一个边界框，通常预测多个边界框。

  例如，通常会预测 2 个或更多边界框。这是因为在实际应用中，目标的大小和形状可以有很大不同，多个边界框可以增加模型捕捉不同形状和大小目标的能力。
  
  - 例如，一个网格单元预测 2 个边界框，每个框都有自己的 `x`、`y`、`w`、`h` 和置信度。
  
  

**YOLOv3代码**

**项目文件**

1. **data：**存放train、val、label数据， trainval.txt指定train数据图片路径合集， 5k.txt指定val数据图片路径合计
2. **cfg：**配置文件， yolov3.cfg：指定各个网络层， data.cfg，指定data数据信息

**data生成器循环加载64个图片数据**

1. **读取train数据：**由生成器加载单张图片 ->  pad到640x640统一大小

2. **读取label标签：**注意debug观察 train和label数据一一对应。标签格式[type, x1, y1, x2, y2]，表示一个框

​	读取标签 -> 将xy转换位pad后的xy -> 计算中心点相对位置，归一化 -> 得到target[type, x, y, w, h]

**Darknet网络**

1. **定义网络层结构：**`def __init__:`，加载网络层配置文件yolov3.cfg，生成网络

1. **确定执行流程:**`def forward:`, 按照函数执行顺序，指定网络层各部分的执行流

------------------------



yolov3.cfg数据格式如下：

定义了三个网络层： conv卷积层 + BN(batchNormalization) + Relu(激活函数)

```python
[convolutional]
batch_normalize=1
filters=32
size=3
stride=1
pad=1
activation=leaky
```

`def __init__` 调用`createNet()`读取配置，创建三个网络层

```python
if module_def["type"] == "convolutional":
            bn = int(module_def["batch_normalize"])
            filters = int(module_def["filters"])
            kernel_size = int(module_def["size"])
            pad = (kernel_size - 1) // 2
            modules.add_module(      #conv
                f"conv_{module_i}",
                nn.Conv2d(
                    in_channels=output_filters[-1],
                    out_channels=filters,
                    kernel_size=kernel_size,
                    stride=int(module_def["stride"]),
                    padding=pad,
                    bias=not bn,
                ),
            )
            if bn:  # bn
                modules.add_module(f"batch_norm_{module_i}", nn.BatchNorm2d(filters, momentum=0.9, eps=1e-5))
            if module_def["activation"] == "leaky":  # relu
                modules.add_module(f"leaky_{module_i}", nn.LeakyReLU(0.1))
```

```py
# 完成拼接操作，参数指向于前面第四层进行拼接
[route]
layers = -4
```

```python
# 残差连接，相加
[shortcut]
from=-3
activation=linear
```

```python
# 上采样
[upsample]
stride=2
```



