---
title: 【Tips】计算某文件夹及其所有子文件夹内的文件数量
date: 2021-09-02 00:55:00
tags: 
- 文件
- 数据集
- Linux
- Python
---

今天处理了 UCF-101 数据集，数据集的文件存储结构大概是这样：

```
- ApplyEyeMakeup
    - v_ApplyEyeMakeup_g01_c01.avi
    - v_ApplyEyeMakeup_g01_c02.avi
    ...
- ApplyLipstick
...
- YoYo
```

在我做了抽取全部帧的处理之后，文件存储结构变成：

```
- ApplyEyeMakeup
    - v_ApplyEyeMakeup_g01_c01.avi
        - 1.jpg
        - 2.jpg
        ...
    - v_ApplyEyeMakeup_g01_c02.avi
    ...
- ApplyLipstick
...
- YoYo
```

目前来看我还不知道这样 抽帧 -> 存储图像 的处理是不是应对这种视频数据集的最好办法（指效率最高），但是应该是可行的。后面考虑怎么生成 Dataset 类以及生成 batch 这样。

在这个过程中我想到一个问题，怎样计算一个文件夹下**所有**的文件数量呢？所有 就是指包括所有子文件夹内部的文件。大致找了三种方法，在 UCF-101 视频数据文件夹（共 13320 个视频）上运行
有肉眼可见的速度差异。

### Linux 命令行 （最快）

```bash
find datasets/UCF-101 -type f | wc -l
```

### Python 使用 os.walk （第二快）

```python
noOfFiles = 0
noOfDir = 0

for base, dirs, files in os.walk("datasets/UCF-101"):
    for directories in dirs:
        noOfDir += 1
    for Files in files:
        # 文件数量
        noOfFiles += 1
```

### Python 递归 （最慢）

```python
def countFile(dir):
    tmp = 0
    for item in os.listdir(dir):
        if os.path.isfile(os.path.join(dir, item)):
            tmp += 1
        else:
            tmp += countFile(os.path.join(dir, item))
    return tmp
```

感觉不同方法的底层实现导致了这里的效率差异。如果之后回顾的时候看到了可以好好分析一下。