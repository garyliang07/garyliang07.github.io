---
layout: post
title: Dissertation- a review of my works
date: 2020-6-20 14:36:30.000000000 +08:00
---

在学业论文系统上点击“提交”之后，好像研究生生涯就要宣告结束了，下面简单总结下成果。

## Dissertation [PDF version](https://drive.google.com/file/d/1c2FCtJN4I5ceeE9NqAOsescBTIXjyBrv/view?usp=drive_link)
- Title: Lattice modeling on fracture behavior of microcapsules embedded in cementitious material  

基于lattice模型的微胶囊在水泥基材料中破裂行为的数值模拟

- Key word：3D lattice modeling; Fracture process; Self-healing; Cementitious materials; Rupture of microcapsules  

三维lattice模型; 断裂过程; 微胶囊自修复; 水泥基材料; 微胶囊破裂

- 基本上是围绕如何建立一个3d水泥-微胶囊系统分析的lattice有限元模型进行论述的，包含一开始的模型稳定性分析，以及参数化的建立过程。

- 参数的获取方面，对于微胶囊（microcapsule）使用的是微观的力学测试方法，如纳米压痕和纳米划痕。而对于水泥，则使用常规的宏观试验进行获取。因此本课题还隐含了**多尺度建模**的前提。

- 由于在商业有限元软件上没有相关的lattice单元选项，因此从网格构建、单元分析到可视化，基本上是通过自己来进行程序编写，**总共超过1000行代码 (大部分使用C++语言，也有部分使用MATLAB及Mathematica)**.

- 因此在成果方面，有相关的**软件著作权**就出自这一部分：  

[1]	王险峰、梁冠熙、韩宁旭、邢锋, 基于lattice模型的有限元分析前处理软件, 软件著作权, 授权号：2019SR055119.  

[2]	王险峰、梁冠熙、韩宁旭、邢锋, MATLAB-ABAQUS耦合优化求解软件, 软件著作权, 授权号：2019SR0877219.

- 这个软件著作权是协助组内学弟进行编写的：  

[1]	王险峰、陈振鹏、梁冠熙、朱继华、邢锋, MATLAB混凝土材料X-CT图像数据处理软件, 软件著作权, 授权号：2020SR0525691.

- 同时也有相应的**论文成果**产出，以及会议上的presentation：  

[1] Liang G X, Wang X F*, Han N X, Xing F. Trigger mechanism of microcapsule based self-healing cementitious material [J]. Materials Science Forum, 2020, 996:91-96.  [PDF](https://drive.google.com/file/d/1qbDdL2-UVRarhmm-7GQW_TNceEL63QWv/view?usp=drive_link)

[2]	梁冠熙, 王险峰*, 钱智炜, 韩宁旭, 邢锋. 微胶囊混凝土的三维lattice模型 [C]. 2019年广东省力学学会学术年会暨广东省力学学会第九届理事会第五次会议, 2019,东莞理工学院, pp.26.

- 这篇论文是首次参与科研活动的产出，当时协助制作所需的micorcapsules：  

[1]	Wang X F*, Huang Y J, Huang Y X, Zhang J H, Fang C, Yu K, Chen Q, Li T, Han R, Yang Z, Xu P, Liang G X, et al. Laboratory and field study on the performance of microcapsule-based self-healing concrete in tunnel engineering [J]. Construction and Building Materials, 2019, 220:90-101.

- 凭借在自己的研究中锻炼出来的**有限元建模和编程能力**，研究生期间参与的两个竞赛均获得了奖项：  

[1]	2018.12 第十五届“华为杯”全国研究生数学建模竞赛三等奖.（**前30%**），题目《对恐怖袭击事件记录数据的量化分析》使用方法为层次分析法、K-聚类分析、BP神经网络、时间序列分析  

[2]	2019.01 广东省力学学会第一届有限元建模竞赛二等奖.（**第二名**），题目[《汽车-护栏系统的有限元建模与分析》](https://drive.google.com/file/d/1jPMHAsdDLTjkkyMm4_y60KBmnckgqMw-/view?usp=drive_link)


- content:

> 第1章 绪论
> 1.1 课题来源
1.2 研究背景和意义
1.3 微胶囊对水泥基材料的自修复研究
1.4 水泥基材料的lattice断裂模拟研究
1.5 现有研究不足之处
1.6 本文研究内容  

> 第2章 三维lattice模型
2.1 引言
2.2 Lattice断裂模型
2.3 lattice断裂分析框架
2.4 本章小结  

> 第3章 Lattice模型的弹性和断裂性能研究
3.1 引言
3.2 随机度的影响
3.4 网格局部加密的影响
3.4.1 弹性性能
3.4.2 断裂性能
3.5 本章小结  

> 第4章 Lattice模型的建立
4.1 引言
4.2 水泥砂浆lattice模型的建立
4.3 微胶囊lattice模型的建立
4.4 水泥砂浆-微胶囊lattice模型的建立
4.5 本章小结  

> 第5章 水泥砂浆中微胶囊破裂过程模拟
5.1 引言
5.2 水泥砂浆-微胶囊模型的拉伸模拟
5.3 微胶囊破裂参数分析
5.4 本章小结  

>第6章 结论与展望
6.1 结论
6.2 展望

## 其他研究成果
- 除了本组的课题之外，还参与了“深圳大学研究生创新基金”的申报，并**连续两届获得资助**，与其他科研人员一起研究力学问题，以下是成果产出：  

[1]	Yang P F, Yang X, Liang G X, Li W W*, Zheng J, Guo S. Applicability Analysis of STM and SMCFT of RC Beams with Shear Span-Depth Ratios ≤ 3.0 [C]. IOP Conference Series: Materials Science and Engineering, 2020.  

[2]	梁冠熙、杨鹏飞、李伟文、唐仕盈, 适用于普通钢筋混凝土梁的简化修正压力场软件, 软件著作权, 授权号：2019SR0608337.  

[3]	李伟文、杨鹏飞、梁冠熙、唐仕盈, FRP加固梁的抗剪承载力计算软件（适用FRP剥离）, 软件著作权, 授权号：2019SR0872912.  

[4]	杨鹏飞、梁冠熙、李伟文、唐仕盈, 简化修正压力场计算软件（适用FRP拉断）, 软件著作权,授权号：2019SR0754826.  

[5]	李伟文、唐仕盈、杨鹏飞、梁冠熙, 一种钢筋混凝土梁柱节点粘贴碳纤维布加固节点, 实用新型专利, 授权号：201921013903.8.
