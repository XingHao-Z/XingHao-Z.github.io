---
title: ADS使用
tags:
  - ADS
  - 仿真
categories:
  - 2-软件
  - 软件使用
date: 2023-10-30 20:56:08
description: Advanced Design System软件使用，包括计算特征阻抗，计算射频线宽，阻抗匹配仿真等
mathjax: true
typora-root-url: ADS使用
---

# 计算射频线宽

## 介绍

PCB射频线一般需要满足特征阻抗为50Ω，可以根据板材介质材料，介质厚度，线的厚度（铜厚），离铺铜的距离等来计算需要的线宽。（或者根据线宽来调整离铺铜的距离）

计算线宽需要使用ADS中的<mark>LineCalc</mark>工具。（还有其他软件也有该功能，如AppCAD，使用方法类似）

LineCalc有两种打开方法，**更推荐第二种**

- 在ADS的任意原理图中，点击tools->LineCalc->Start LineCalc

![](image-20231030210844623.png)

- 开始菜单，点开Advanced Design System，点击LineCalc

![](image-20231030211132105.png)

射频走线一般都是接地共面波导的模型，所以先将Type改为CPWG，界面如下：

![](image-20231030212108446.png)

左边的方框主要为板材的基本信息：

- Er：板材介质的介电常数
- H：板材介质的厚度
- T：走线（铜皮）的厚度
- TanD：板材介质的损耗因子（损耗角正切）
- 其他参数一般保持默认即可，想知道具体含义参考《ADS2011射频电路设计与仿真实例》p82

左下的方框为工作频率。

中间上边W为线宽，G为离地的间距，在计算时，需要固定其中一个值（L不用管），中间下边Z0为特征阻抗。

中间往上的箭头为根据Z0计算W或G，往下的箭头为根据W和G计算Z0.

## 示例

<mark>示例</mark>：（即上图）

板材材料选择RoGers4350

![](image-20231030213534612.png)

![](image-20231030213622828.png)

该材料介电常数**Er**的电路设计推荐值为：3.66

损耗因子**TanD**：因为工作频率为6G，所以我取了中间值，0.0034。（实际LineCalc只保留三位小数）

厚度**H**选择若干推荐标准厚度中的0.51mm

走线厚度**T**：选择AD的默认厚度0.036mm

频率6GHz

特征阻抗**Z0**为50

固定**G**为20mil，点击上箭头，计算出**W**为40mil左右。

固定**W**为40mil，点击上箭头，计算出**G**为21.4mil。

就可根据该规则来布局布线。

# AD的PCB导入ADS仿S参数

参考资料：[altium designer PCB 导入ADS EM仿真](https://blog.csdn.net/luohuo9844/article/details/107369332)

1. **AD导出ODB++文件**

   打开AD→file（文件）→ fabrication output（制造输出） → ODB++ files

   绘制层→关闭所有→确定

   ![](image-20231031225142912.png)

   出现以下图片，确定。（还会生成并弹出.Cam文件，可以直接关掉不保存）

   ![](image-20231031225459731.png)

   项目文件夹中会出现Project Outputs for LineSim文件夹

   ![](image-20231031225659512.png)

   点开内容如下，等会儿会用到其中的.zip压缩文件

   ![](image-20231031225730701.png)

2. **导入到ADS**

   打开ADS → 新建workspace → New Layout Window，选择mil为单位

   ![](image-20231031230550022.png)

   点击New Layout Window时，由于版本原因可能出现：

   ![](image-20231031230230943.png)

   点Cancel，再按提示如下修改即可，

   ![](image-20231031230330794.png)

   建好的layout界面如下：

   ![](image-20231031230728864.png)

   该界面，点击 File → import，选择ODB++ file format。

   <mark>注</mark>：若出现ODB++ file format（legacy）选项，说明ADS版本较新，ODB++ file format选项与老版本的有差别，应该选择ODB++ file format（legacy）选项。

   ![](image-20231031230930981.png)

   Import file name选择刚才AD导出的Project Outputs for LineSim文件夹中的压缩文件，点击options

   ![](image-20231031231406643.png)

   这里仿真不能有器件，所以component都要去掉，只仿线

   ![](image-20231031231756705.png)

   点击OK，出现以下界面：

   ![](image-20231031232310755.png)

   框出来的部分根据实际情况修改。thickness导进来有的会变很多。Dielectric Constant为介质介电常数，Loss Tangent为损耗因子（损耗角正切）

   点击OK

   ![](image-20231031232435448.png)

   点击OK，打开layout，导入效果如下（这里发现AD中忘了铺铜）

   ![](image-20231031232642610.png)

3. 切板子（可选），添加端口port，设置仿真

   如果PCB板太大，仿真时间会大大增加，只需要需要仿真的线的周围部分即可。

   切换到top层，选中要仿真的线，点击EM → tools → Cookie Cutter

   ![](image-20231031233445497.png)

   输如要切的范围，点击cut

   ![](image-20231031233543543.png)

   会生成新的layout界面，如下

   ![](image-20231031233640303.png)

   放置端口，点击端口放在线两边（ctrl+R旋转）

   ![](image-20231031233854213.png)

   点击port editor，修改Gnd Layer为PCB板中的地层

   ![](image-20231031234033247.png)

   新建仿真设置

   ![](image-20231031234144414.png)

   修改Frequency plan为要仿真的频段，例子如下：

   ![](image-20231031234312572.png)

   根据参考资料，把下图也勾上了，但似乎影响不大

   ![](image-20231031234439817.png)

   设置完就可以点击仿真设置界面右下角的simulate仿真了，或者点击下面的图标仿真

   ![](image-20231031234655120.png)

4. 其他操作

   - 修改移动精度。

     默认的移动精度较大，不好调整位置

     在option→Grid Spacing下调整

     ![](image-20231101151032940.png)

   - 测量间距

     insert→ruler

     放好后，鼠标滑轮放大可以看到刻度，读出距离

