---
title: "机器人关节系统设计"
date: 2024-03-01
---
## 功能
### 动力传递：转速和转矩

### 能量转换
* 电能，磁能
* 机械能
    * 动能
    * 噪声
* 内能

### 信息控制：反驱（back-drive）

## 原动机（电动机）
### 伺服控制
* 执行器
* 控制器
    * 固件、程序、算法
* 传感器
    * 角度位置传感器
    * 高、低速端双反馈

### 电能转换
* DC稳压直流源
* BL无刷
* 三相逆变器
    * 主电路
    * 驱动电路
    * 隔离电路
    * 检测电路
    * 控制电路
    * 保护电路

### 电磁转化
* 三相集中式分数槽2/7绕组
* 铁芯（空芯杯亦可）

### 磁能与动能
* PMSM永磁体励磁
* 磁路结构
    * 径向磁通
    * 轴向磁通
    * 复杂三维磁路

## 传动机
* 传递转速和转矩
* 摩擦力
* 形式
    * 行星减速器
    * 摆线减速器
    * 谐波减速器

## 维稳系统
为原动机和传动机构建并维持一个长期良好的环境，使其发挥出设计性能的基础子系统（类似维生系统）
* 轴承：保证回转件运行
* 温控散热器：维持环境温度
    * 过温退磁
    * 电子器件老化
* 机械本体
    * 机壳：抵御外界干扰
    * 连接件：保证动力传递可靠
    * 定位紧固件
        * 保证传感器精度
        * 保证轴承长期工作
        * 保证系统完整，在设计寿命内不失效

## 软件
* Encoder模块：获取高速编码器位置和角度
* Hall模块：低速侧位置反馈处理
* 电流AD测量模块
* 控制模块：FOC，电流环、力矩环
* PWM模块：SPWM发生->SVPWM
* 校准模块：高低速侧编码器位置对齐，ABC三相校准，编码器偏心校准
* DRV8323模块：通信、配置、状态读取和保护
* 保护程序：过压、过流、过温，8323状态，编码器状态，FOC状态
* 通信模块：CAN/Ethercat
* 串口通信：高低速侧编码器，debug串口，配置校准CMD
* 参数存取：片上Flash，永久参数（磁极对数、板子ID），电机相关参数（编码器偏移值等）

### 功能
* 硬件自检
* 开机时间优化
* 故障保护优化
* 日志上传优化
* 硬件上电状态管理
* 软件启动状态管理

### 调试工具
* 下载工具：SWD
* 通信接口：CAN，CAN-FD，DEBU串口
* CAN工具
    * 单通道Peak分析仪
    * 4通道CAN分析仪
* 串口工具：USB-TTL
* 上位机软件
* 工业以太网分析仪

## 设计流程
1. 设计目标

2. 电磁设计
* 电磁设计，仿真建模
* 构建代价函数
* 选择合理的优化算法
* 求多个局部最优解

3. 散热设计
* 散热设计，热仿真建模
* 构建代价函数
* 选择合理的优化算法
* 求多个局部最优解

4. 结构设计
* 结构设计，强度及振动仿真建模
* 构建代价函数
* 选择合理的优化算法
* 求多个局部最优解

5. 构建关节设计代价函数

6. 选择合理的优化算法

7. 得到全局最优解

## 测试
* T-N曲线
* 效率Map
    * 驱动器效率
    * 电机效率
    * 传动效率
* 温度
* 噪声
* 测试装备&设备
    * 测功机
    * 功率分析仪
    * 对拖台架
