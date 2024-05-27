---
title: VDJtools
date: 2023-08-31 11:44:18
categories: 
- 软件算法
- 生信
tags: ['技术','个人成长']
hide: false
---
10X免疫组知识补充（VDJtools）
<!-- more -->
## 工作流程
![](framework.png)
vdjtools 是一款基于 java 语言的， 借助 R 语言及相应的模块快速进行免疫组库分析软件(绘图都是基于R包)。
[vdjtools 官网链接](https://vdjtools-doc.readthedocs.io/en/master/index.html)

## 输入文件 Clonotype tables
- 可变 ( V ) 段名称。
- D 段名称：一些受体链（TRB、TRD 和 IGH）的多样性 ( D ) 片段名称。如果不适用或未识别 D
段，设置为 . 或者 NA。
- 加入 ( J ) 段名称。
- 互补决定区 3 核苷酸序列 ( CDR3nt )。CDR3 以可变区参考点（保守的 Cys 残基）开始，以连接片
段参考点（保守的 PheTrp）结束。
- 翻译后的 CDR3 序列 ( CDR3aa )。
- 可变区段中的体细胞超突变 (SHM )（仅限抗体）

克隆型丰度数据由 计数 和 频率 字段表示：
- 计数：umis 数量
- 频率：样本中克隆型的比例（umis 数量/总 umis 数量）

以下字段是可选的，但用于计算各种统计数据和可视化：
- Vend、Dstart、Dend 和 Jstart：标记CDR3核苷酸序列的V、D、J段边界

**输入文件格式**
![](输入文献格式.png)

**metadata表格(以tab键分割)**
![](metadata.png)
- file_name 和 sample_id两列是必须的。 其余列的名称将用于指定metadata 变量名。
- 前两列应分别包含文件名和样本 ID。（文件名应为绝对路径或相对于metadata表格的相对路径；样本ID必须是唯一的）
- sample.id之后的列被视为 metadata 条目。后续作图时可以被调用。

## [功能模块](https://vdjtools-doc.readthedocs.io/en/master/modules.html)
