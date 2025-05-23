---
title: QTcreator上位机
date: 2023-10-09 12:25:13
tags:
 - QTCreator
 - 上位机
 - 软件打包
categories:
 - 2-软件
 - 软件使用
description: 使用QTcreator编写上位机的相关内容，包括：重复的代码模板、工程设置、打包程序等
---

- 让字体适应高分辨率，在`main`函数开始加以下语句：

  ```cpp
  QCoreApplication::setAttribute(Qt::AA_EnableHighDpiScaling);
  ```
  
- 检查QByteArray每个字节的bit

  ```cpp
  QByteArray byteData;
  const char *pData = byteData.constData();
  for (int i = 0; i < byteData.size(); ++i) {
      for (int j = 7; j >= 0; --j) {
          if (pData[i] & (1 << j)) {
              std::cout << "1";
          } else {
              std::cout << "0";
          }
      }
      std::cout << std::endl;
  }
  std::cout << "--------------------" << std::endl;
  ```

- QByteArray通过SerialPort.wirte()发送时，是从下标为0的字节开始发送，每个字节内是从低位开始发送

- 更换图标，将.ico放到工程文件夹内，在.pro中添加

  ```c++
  RC_ICONS = xxxxxx.ico
  ```

- 打包可执行文件：

  - 构建切换到Release模式，点击运行

  - 在build-xxxxx-Release文件夹中的release文件夹中找到xxx.exe，复制到新创建的一个文件夹（如MyEXE）中，

  - 开始菜单搜索qt，打开命令窗口，用" <mark>cd /d 路径</mark> "切换到MyEXE下，例如

    ```
    cd /d F:\projects\qtcreator\MyEXE
    ```

  - 再输入：windeployqt xxx.exe

    ```
    windeployqt xxx.exe
    ```

  - 打包完成，已经可以正常使用了。接下来借用其他软件将所有文件打包到一个exe文件

  - 打开Enigma Virtual Box，选择刚才打包好的exe文件，点击增加，增加刚才新创建的文件夹（如MyEXE），点击“文件选项”，勾选压缩文件，确定，执行封包，等待，最后就可以得到只有一个可以运行的exe文件

![](image-20230412122755410.png)
