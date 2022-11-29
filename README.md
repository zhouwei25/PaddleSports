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


## 1. [*when*](./01-sports_when/)
乒乓球demo加载中...:movie_camera:
<div align="center">
  <img src="./image/乒乓球.gif" width="550px"/><br>
</div>

&emsp; “when”模块重点从时域角度回答以下问题：

&emsp; 1）输入一段视频，首先判断是什么体育运动；

&emsp; 2）从一段视频中，精确分割出体育运动的起止时间；

&emsp; 3）判断每一帧属于哪个动作，以跳水三米板为例，动作过程分为：走板、起跳、空中、入水等阶段。

&emsp; 4）时间同步，针对多相机同步问题，整理了硬件同步和软件同步两种控制方法。

&emsp; 5）编解码，包括视频编解码和音频编解码。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 1.when          | 1.1) 视频分类          | 视频分类（是什么体育项目）               | PP-TSM                                              |
|                 |                    |                             | PP-TimeSformer                                      |
|                 |                    |                             | SlowFast                                            |
|                 |                    |                             | AttentionLSTM                                       |
|                 |                    |                             | MoViNet                                             |
|                 | 1.2) 视频分割          | 片段切割（起始点，终止点）               | BMN                                                 |
|                 | 1.3) 视频理解          | 动作识别（每一帧属于什么动作）             | MS-TCN                                              |
|                 |                    |                             | CFBI                                                |
|                 |                    |                             | ASRF                                                |
|                 | 1.4) 硬件同步          | 硬件同步                        | PTP同步，IEEE 1588                                     |
|                 |                    | 软件同步                        | CPU时钟同步                                             |
|                 | 1.5) 编解码           | 视频编码                        | H.264/MPEG-4 AVC                                    |
|                 |                    | 音频编码                        | WAV/MP3/AAC                                         |
|                 |                    |                             |                                                     |




## 2. [*where*](./02-sports_where/)

&emsp; “where”模块重点分析：前景（运动员）、背景（场馆）、相机，这三类对象的位置/位姿的信息：

&emsp; 1）运动员整体位姿：图像/视频中运动员的2D/3D定位，包含：2D/3D检测、2D分割、2D/3D跟踪等；

&emsp; 2）运动员局部位姿：运动员的骨骼姿态的分析，从粗粒度到细粒度，包含：2D骨骼关键点、2D骨骼姿态、3D骨骼姿态、2D-3D稠密映射、3D人体重建、3D人体动画等；

&emsp; 3）背景3D重建：利用多维传感器数据，1比1重建场馆的3D信息，相关技术包含：Simultaneous Localization and Mapping (SLAM)、Structure-from-Motion (SfM) 等；

&emsp; 4）相机6-DoF位姿：恢复相机的6-DoF位姿（位置xyz，旋转αβγ），有经典的PNP算法，以及深度模型算法。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 2.where         | 2.1) 2D检测          | 一阶段通用目标检测                   | PP-YOLOE                                            |
|                 |                    |                             | PP-PicoDet                                          |
|                 |                    | 二阶段通用目标检测                   | Faster-RCNN                                         |
|                 |                    | 人体检测分析                      | PP-Human2.0                                         |
|                 |                    |                             | PP-Pedestrian                                       |
|                 |                    | 水花/足球/篮球等小目标检测              | FPN，PP-YOLOE                                        |
|                 |                    |                             |                                                     |
|                 | 2.2) 2D分割          | 前景对象/背景分割                   | Mask-RCNN                                           |
|                 |                    |                             | SOLOv2                                              |
|                 |                    |                             | PP-LiteSeg                                          |
|                 |                    |                             | DeepLabV3P                                          |
|                 |                    | 交互式分割                       | EISeg                                               |
|                 |                    | 人体分割                        | PP-HumanSeg                                         |
|                 |                    | 人体毛发级精准分割                   | Matting                                             |
|                 |                    |                             | Human Matting                                       |
|                 |                    | 视频目标分割                      | CFBI                                                |
|                 |                    |                             | MA-Net                                              |
|                 |                    | 视频运动物体分割                    | Motion Segmentation                                 |
|                 |                    | 视频人体分割 Video Matting        | BackgroundMattingV2                                 |
|                 |                    |                             |                                                     |
|                 | 2.3) 2D跟踪          | 人体跟踪                        | ByteTrack                                           |
|                 |                    | 运动轨迹                        | PP-Tracking                                         |
|                 |                    |                             |                                                     |
|                 | 2.4) 2D骨骼          | Top-Down                    | PP-TinyPose                                         |
|                 |                    |                             | HR-Net                                              |
|                 |                    | Bottom-Up                   | OpenPose                                            |
|                 |                    |                             | MoveNet                                             |
|                 |                    |                             |                                                     |
|                 | 2.5) 3D骨骼          | 单目                          | PP-TinyPose3D                                       |
|                 |                    |                             | Position-based                                      |
|                 |                    |                             | Angle-based                                         |
|                 |                    |                             | 2D + Depth-based                                    |
|                 |                    |                             | 2D + IK                                             |
|                 |                    | 多目                          | Calibration                                         |
|                 |                    |                             | Fusion                                              |
|                 |                    | 深度相机                        | Kinect 3D Tracking                                  |
|                 |                    |                             |                                                     |
|                 | 2.6) 2D/3D稠密映射     | 2D-2D Dense Correspondences | DeepMatching                                        |
|                 |                    | 2D-3D Dense Correspondences | DensePose                                           |
|                 |                    |                             |                                                     |
|                 | 2.7) 3D人体重建        | Template Model              | SMPL                                                |
|                 |                    |                             | VIBE                                                |
|                 |                    |                             | PyMaf                                               |
|                 |                    |                             |                                                     |
|                 | 2.8) SLAM          | 静态                          | 单目 ORB-SLAM...                                      |
|                 |                    |                             | 深度 KinectFusion...                                  |
|                 |                    |                             | 激光 LOAM                                             |
|                 |                    | 动态                          | DynamicFusion                                       |
|                 |                    |                             | DynSLAM                                             |
|                 |                    |                             |                                                     |
|                 | 2.9) 相机6-DoF定位     | 内参                          | 张氏标定法                                               |
|                 |                    | 外参                          | 单张图像 PNP                                            |
|                 |                    |                             | 多张图像 SfM, SLAM                                      |
|                 |                    |                             |                                                     |



## 3. [*who*](./03-sports_who/)


&emsp; “who”模块重点分析：图像/视频中有哪几类人员，分别是谁，特定人员在整场比赛的集锦等信息：

&emsp; 1）人员分类：把图像/视频中运动员、观众、裁判、后勤工作人员进行区分；

&emsp; 2）运动员识别：识别出特定运动员，包含：人脸识别、人体识别、号码簿识别等；

&emsp; 3）运动员比赛集锦：自动生成该运动员整场比赛的视频集锦。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 3.who           | 3.1) 人员分类          | 运动员、裁判、观众、后勤人员              | PP-LCNetV2.md                                       |
|                 | 3.2) 运动员识别         | 人脸检测                        | BlazeFace                                           |
|                 |                    | 人脸识别                        | Dlib                                                |
|                 |                    | 基于人体的运动员识别                  | Re-ID                                               |
|                 | 3.3) “一人一档”        | 运动员Re-ID                    | MultiSports                                         |
|                 |                    |                             |                                                     |


## 4. [*what*](./04-sports_what/)

&emsp; “what”模块重点分析体育比赛画面中呈现的信息，包含：运动、语音、视觉、多模态等：

&emsp; 1）运动属性，从视频前后帧信息推断运动信息，包含2D光流以及3D场景流相关技术；

&emsp; 2）语义属性，包含：图像/视频检索识别，视频动作识别，image/video caption等；

&emsp; 3）视觉属性，包含：画质增强，超分辨率，2D转3D，3D实时交互等；

&emsp; 4）多模态属性，视觉数据与语音数据、文本数据联合分析。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 4.what          | 4.1) 运动属性          | 2D Optical Flow (经典算法)      | Horn-Schunck光流法                                     |
|                 |                    |                             | Lucas-Kanade光流法                                     |
|                 |                    |                             | Block-Matching光流法                                   |
|                 |                    |                             | Dual-TVL1                                           |
|                 |                    |                             | DeepFlow-v2                                         |
|                 |                    |                             | Global Patch Collider                               |
|                 |                    | 2D Optical Flow (深度学习)      | RAFT (ECCV 2020 best paper)                         |
|                 |                    |                             | FlowNet1.0                                          |
|                 |                    |                             | FlowNet2.0                                          |
|                 |                    |                             | NVIDIA SDK                                          |
|                 |                    | 3D Scene Flow               | FlowNet3D                                           |
|                 |                    |                             | Just Go with the Flow                               |
|                 |                    |                             | MotionNet                                           |
|                 |                    |                             | 2D-3D Expansion                                     |
|                 | 4.2) 语义属性          | 图像检索识别                      | PP-Lite-Shitu                                       |
|                 |                    |                             | PP-LCNetV2                                          |
|                 |                    | 视频动作识别                      | CTR-GCN                                             |
|                 |                    |                             | ST-GCN                                              |
|                 |                    |                             | AGCN                                                |
|                 |                    | Image Caption               | COCO Caption                                        |
|                 |                    |                             | Im2Text                                             |
|                 |                    | Video Caption               | ActivityNet                                         |
|                 |                    | OCR                         | PaddleOCR                                           |
|                 | 4.3) 视觉属性          | 画质增强                        | Space-Time-Aware Multi-Resolution Video Enhancement |
|                 |                    | 图像/视频去噪                     | FastDVDnet                                          |
|                 |                    | 超分辨率                        | Super Resolution                                    |
|                 |                    | 图像填补                        | Inpainting                                          |
|                 |                    | 2D转3D                       | NeRF                                                |
|                 |                    | 3D Visualization            | Maya                                                |
|                 |                    |                             | Unity                                               |
|                 |                    |                             | Unreal                                              |
|                 | 4.4) 多模态属性         | 文本+视觉                       | VideoBERT                                           |
|                 |                    |                             | VisualBERT                                          |
|                 |                    |                             |                                                     |



## 5. [*why*](./05-sports_why/)

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




## 6. [*how*](./06-sports_how/)

&emsp; “how”模块重点分析影响“AI+Sports”技术落地的因素：

&emsp; 1）费用，取决于数据标注数量和网络训练需要的GPU费用；

&emsp; 2）人力，重新训练模型所需的人力数量；

&emsp; 3）时间，配置、测试、重训练、重开发等所需要的时间。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 6.how           | 6.1) much          | 经费                          |                                                     |
|                 | 6.2) many          | 人力                          |                                                     |
|                 | 6.3) long          | 时间                          |                                                     |
|                 |                    |                             |                                                     |




## 7. [*data*](./07-data/)

&emsp; “data”模块重点梳理生成训练数据的6种主流方式：

&emsp; 1）人工标注：已标注的公开数据集，用于网络训练；

&emsp; 2）迁移学习：未标注的大量数据，做非监督学习和迁移学习；

&emsp; 3）合成数据：2D图像直接编辑，copy-paste的方式合成训练数据；

&emsp; 4）合成数据：3D模型渲染生成2D数据以及标注信息；

&emsp; 5）合成数据：3D模型部件指导的2D图像编辑；

&emsp; 6）合成数据：GAN系列网络模型合成训练数据。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 7.data          | 7.1) 已标注的数据集       |                             |                                                     |
|                 | 7.2) 未标注的数据集       |                             |                                                     |
|                 | 7.3) 2D Copy-Paste |                             |                                                     |
|                 | 7.4) 3D Rendering  |                             |                                                     |
|                 | 7.5) 3D-2D Editing |                             |                                                     |
|                 | 7.6) GAN           |                             |                                                     |
|                 |                    |                             |                                                     |



## 8. [*benchmark*](./08-benchmarks/)

&emsp; “benchmark”模块将构建第一个体育类的benchmark，尽可能让所有算法在一个数据集上进行评测，特点是小而精，包含以下信息：

&emsp; 1）when：时域信息标注，回合起止节点；

&emsp; 2）where：2D/3D检测，2D分割，2D跟踪，2D/3D骨架；

&emsp; 3）who：人员分类，姓名；

&emsp; 4）what：运动，语义，视觉信息。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 8.benchmark     | 8.1) 训练数据集         |                             |                                                     |
|                 | 8.2) 测试数据集         |                             |                                                     |
|                 | 8.3) 评估脚本          |                             |                                                     |
|                 |                    |                             |                                                     |


## 9. [*tools*](./09-tools/)

&emsp; 面向体育场景的工具集，比如标注工具、检测工具、识别工具等，具有All-in-One，AutoRun的特点。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 9.tools         | 9.1) 标注工具          |                             |                                                     |
|                 | 9.2) 检测工具          |                             |                                                     |
|                 | 9.3) 识别工具          |                             |                                                     |
|                 | 9.4) 深度图生成工具       |                             |                                                     |
|                 |                    |                             |                                                     |

## 10. [*applications*](./10-applications/)

&emsp; 涵盖足球、跳水、乒乓球、花样滑冰、健身、篮球、蹦床、大跳台、速度滑冰、跑步等热门的体育运动。

| 任务              | 技术方向               | 技术细分                        | 算法模型                                                |
|-----------------|--------------------|-----------------------------|-----------------------------------------------------|
| 10.applications | 10.1) 足球           | Tracking，ReID               |                                                     |
|                 |                    | 比分牌识别                       |                                                     |
|                 |                    | 超分辨率                        |                                                     |
|                 |                    | 动作识别+增强版                    |                                                     |
|                 |                    | 检测+识别+跟踪+足球                 |                                                     |
|                 | 10.2) 跳水           |                             |                                                     |
|                 | 10.3) 乒乓球          |                             |                                                     |
|                 | 10.4) 花样滑冰         |                             |                                                     |
|                 | 10.5) 健身           |                             |                                                     |
|                 | 10.6) 篮球           |                             |                                                     |
|                 | 10.7) 蹦床           |                             |                                                     |
|                 | 10.8) 大跳台          |                             |                                                     |
|                 | 10.9) 速度滑冰         |                             |                                                     |
|                 | 10.10) 跑步/舞蹈       |                             |                                                     |
|                 |                    |                             |                                                     |

# 合作伙伴
- 国家队
- 央视
- 国家体育总局体育科学研究所，河北省体育科学研究所
- 高校：厦门大学，南京大学，北京航空航天大学，上海科技大学，大连理工大学等
- 商业公司：Intel，Sony，Pixellot，全度科技等

# 百度开发团队
- 百度研究院 机器人与自动驾驶实验室（RAL）
- 百度研究院 大数据实验室（BDL）
- 百度深度学习技术平台部（PaddlePaddle）
- 百度ACG产业创新业务部
- 百度研究院 GAIT实验室

# 致谢
感谢飞桨兴趣小组（PPSIG）Models-CV成员对PaddleSports建设的贡献（张熙瑞，洪力，王成，卜宜凡，孔远杭，肖培楷，张戈等）
