# PaddleSports

# 框架介绍
PaddleSports是飞桨面向体育场景的端到端开发套件，实现人工智能技术与体育行业的深度融合，目标打造“AI+Sports”的标杆案例集。PaddleSports的特色如下：

1. 整体采用“5W1H”的产品架构，即：[*when*](#1-when)（什么时间），[*where*](#2-where)（什么位置），[*who*](#3-who)（是谁），[*what*](#4-what)（发生了什么），[*why*](#5-why)（为什么），[*how*](#6-how)（怎么样）。系统梳理人工智能技术在体育行业的研究、应用、落地。

2. *AI模型*：从精度、速度、集成度三个维度进行性能评测。AI技术不仅是深度学习，同时整理了经典3D建模，SLAM，机器学习，以及硬件集成开发等工作，目标打造软硬一体的“AI+Sports”开发套件。

3. [*数据*](#7-data)：除了各个已有的公开数据集来评测深度模型的性能外，将首次推出[*SportsBenchmark*](#8-benchmark)，力争能够用一个数据集来评测所有算法模型。

4. [*工具*](#9-tools)：面向体育场景的工具集，比如标注工具、检测工具、识别工具等，具有All-in-One，AutoRun的特点。

5. [*应用*](#10-applications)：涵盖足球、跳水、乒乓球、花样滑冰、健身、篮球、蹦床、大跳台、速度滑冰、跑步等热门的体育运动。


# 分模块介绍
该部分详细介绍“5W1H”各个模块的内容。



## [*why*](./05-sports_why/)

&emsp; “why”模块重点分析影响运动表现的因素，并尝试预测伤病的可能性、比赛成绩等：

&emsp; 1）采集生理、心理、体能相关数据，并与运动表现进行关联性分析；

&emsp; 2）从生物力学的角度，对动作细节进行纠正；

&emsp; 3）从内负荷、外负荷的角度，在确保训练强度的情况下，尽可能减少伤病发生的可能性。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 5.why           | 5.1) 分析            | 技术、生理、心理、体能                 |                                                     |
|                 | 5.2) 推理            | 生物力学                        |                                                     |
|                 | 5.3) 预测            | 内负荷、外负荷                     |                                                     |
|                 |                    |                             |                                                     |
