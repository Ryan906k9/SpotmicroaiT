# 项目概述

本项目是基于 SpotMicroAI 机器狗开发项目。

项目预期分为三个阶段：

1. 按照 SpotMicroAI 构建机械结构和遥控体系。
2. 使用模拟器，基于强化学习训练专属的步态。
3. 添加摄像头等感知装置，实现机器狗自行避障。
4. 增加目标检测算法，实现机器狗跟随模式。

# 第一阶段

## 1. 构建 3d 结构

遇到的问题：

1. 3D 打印没有设置支撑
2. 3D 打印支撑结构去除困难
3. 3D 打印后拼接困难
4. 使用的螺丝型号无法确定
6. 舵机和机械结构要同步安装，否则有些地方固定了舵机装不进去

## 2. 连接电子元件

元件目录：

1. 树莓派 3b
2. TF（MicroSD）卡 32G
3. TF 卡读卡器
4. 杜邦线
5. PCA9685 舵机控制板 * 2
6. 平头 18650 锂电池 2600mAh * 4
7. 18650 锂电池专用电池盒（容量4节电池）
8. DC-DC 可调降压模块 * 2
9. MG996R 舵机 * 12
10. 蓝屏 LCD1602+I2C
11. KCD1 开关

机械元件：

1. 螺丝
2. 轴承（内径 d=5mm，外经 D=16mm）* 8

工具：

1. 热熔胶枪
2. 热熔胶
3. 螺丝刀

额外元件：

1. 树莓派 3b 铝合金散热外壳（带风扇）


遇到的问题

1. LCD 屏幕购买错误，只买了裸屏，没有 I2C 模块
2. 开关型号错了，尺寸对不上开孔，需要KCD1，对应开孔尺寸 20mm*13mm 左右
3. 电源模块莫名其妙就坏了，应该是 5v 的输出，结果直接等于输入电压了
4. xbox360 的手柄无法使用
5. PS4 的手柄，可以连上，但是一旦关机后再打开，树莓派显示连接上，但是手柄显示未连接
6. 原始教程的电路连接上 SCL 和 SDA 接反了
7. 开关的连接可以用焊接，缠绕，或者冷压端子
8. 购买了树莓派专用的无线键盘作为手柄的替代品，后面软件设置还有待研究怎么修改



## 3. 软件系统搭建

遇到的问题

1. 两块 PCA9685 由于型号一样，所以硬件地址一样，导致 I2C 控制的时候出了问题
2. 安装 RPi.GPIO 报错
3. 需要针对新的无线键盘修改程序，原来的程序是针对蓝牙连接的，但现在的连接方式是2.4g

## 4. 舵机校准

遇到的问题

1. import busio 报错
2. 输入角度后舵机转动，但是这并没有完成校准

通过输入对应的角度尝试，让舵机转动到我们需要的 rest 时候的位置，然后记录下这个时候的角度值
并将该值写入到 json 文件中
这样确保机器狗启动的时候，即 rest 状态的时候，可以读取到正确的角度位置。