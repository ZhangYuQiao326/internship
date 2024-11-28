# 环境搭建

1. 拷贝目录文件到服务器
2. conda 创建虚拟环境，要求python = 3.9以上

```shell
conda create -n py39_env python=3.9 -y
```

3. 环境进入yolo8根目录，安装依赖

```shell
pip install ultralytics
conda activate py39_env
```

4. 





# 一 目录结构

## 1.0 参考博客

[目录、基本运行讲解](https://luqu8.top/2024/09/25/article_1/)

[调参技巧](https://www.cnblogs.com/harrychinese/p/17973306)

## 1.1 功能

> cfg -- yaml文件， 存放模型的总参数 和 模块参数

> engin --  model.py 设置模型的功能(训练、预测)

> nn -- 任务的具体实现（分类、检测、切割）和 具体的模块实现（根据yaml构建）

## 1.2 模型启动流程

`models/default.ymal`

1 创建模型，`ultralytics/engine/model.py __init__()`

选择模型mode执行task函数

| 参数   | 调用参数                                                     |
| ------ | ------------------------------------------------------------ |
| `task` | 具体任务模型，调用对应的函数`nn/tasks.py`                    |
| `mode` | 模式（train、val、predict），`ultralytics/engine/model.py/train()`，函数内调用task |
| ``     |                                                              |
| ``     |                                                              |

2 `nn/tasks.py`

模型模块的初始化和定义

| 任务         | 任务函数                                  |
| ------------ | ----------------------------------------- |
| 基础模型任务 | `class BaseModel(nn.Module)`              |
| 检测         | `class DetectionModel(BaseModel)`         |
|              | `class OBBModel(DetectionModel)`          |
| 分割         | `class SegmentationModel(DetectionModel)` |
| 姿态         | `class PoseModel(DetectionModel)`         |
| 检测         | `class ClassificationModel(BaseModel)`    |
|              |                                           |

