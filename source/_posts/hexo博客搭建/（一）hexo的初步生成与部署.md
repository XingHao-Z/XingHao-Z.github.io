---
title: （一）hexo的初步生成与部署
date: 2023-10-3 22:45:15
tags:
 - hexo
 - 博客
categories:
 - hexo博客搭建
description: 记录在window下使用hexo搭建博客的步骤。本节介绍内容：搭建前的准备；初步生成一个具有默认界面博客；免费部署到GitHub上。
typora-root-url: （一）hexo的初步生成与部署
---

参考资料：[hexo史上最全搭建教程](https://blog.csdn.net/sinat_37781304/article/details/82729029)

# 1、注册GitHub

​	本博客最终免费部署到GitHub上，所以需要GitHub账号。[GitHub](https://github.com/)

​	没有的可以注册一个GitHub账号。

​	<mark>记住GitHub的用户名和邮箱</mark>

# 2、安装Git

​	Git是目前世界上最先进的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。这也是用来管理你的hexo博客文章，上传到GitHub的工具。廖雪峰老师的Git教程写的非常好：[Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)。可以简单了解下什么是Git，不需要深入了解Git的相关知识，要用什么直接上网查即可。

​	到git官网上下载windows版本，[Download for Windows](https://git-scm.com/download/win),下载安装后会有一个Git Bash的命令行工具，以后就用这个工具来使用git。

​	安装步骤参考：[Git 详细安装教程](https://blog.csdn.net/mukes/article/details/115693833)

![image-20230717204215864](image-20230717204215864.png)

![image-20230717204412095](image-20230717204412095.png)

![image-20230717204503188](image-20230717204503188.png)

![image-20230717204556024](image-20230717204556024.png)

​	这里选择了vscode作为默认编辑器。也可以选择默认的Vim。选择vscode需要先下载vscode再进行下一步，还要在`我的电脑->属性->高级系统设置->高级->环境变量->系统变量->Path->编辑添加`（其实这步的设置默认编辑器暂时即可，在后续的整个搭建中还没有遇到需要使用这个的情况，仅仅是因为本人对vscode熟悉，所以设置成了vscode）

![image-20230717204748855](image-20230717204748855.png)

![image-20230717205646513](image-20230717205646513.png)

![image-20230717210153103](image-20230717210153103.png)

![image-20230717210230985](image-20230717210230985.png)

![image-20230717210310753](image-20230717210310753.png)

![image-20230717210341151](image-20230717210341151.png)

![image-20230717210354519](image-20230717210354519.png)

![image-20230717210441597](image-20230717210441597.png)

![image-20230717210525764](image-20230717210525764.png)

![image-20230717210539598](image-20230717210539598.png)

![image-20230717210617763](image-20230717210617763.png)

![image-20230717210628362](image-20230717210628362.png)

![image-20230717210920155](image-20230717210920155.png)

在开始菜单应用里打开`Git Bash`，输入`git --version` 查看版本，检查是否安装成功

```
git --version
```

![image-20230717211651140](image-20230717211651140.png)

![image-20230717211850855](image-20230717211850855.png)

将Git和GitHub账号绑定，分别输入以下命令：

```
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```

![image-20230717213051803](image-20230717213051803.png)



# 3、安装Node.js

Hexo是基于nodeJS编写的，所以需要安装nodeJs和里面的npm工具。[nodejs](https://nodejs.org/en/download/) 选择LTS版本就行了。

![image-20230717213233534](image-20230717213233534.png)

![image-20230717213247366](image-20230717213247366.png)

![image-20230717213323064](image-20230717213323064.png)

![image-20230717213337988](image-20230717213337988.png)

![image-20230717213456752](image-20230717213456752.png)

![image-20230717213508007](image-20230717213508007.png)



# 4、安装hexo

官网主页简单说明了会使用到的命令，下面详细说明：

![image-20230719220206586](image-20230719220206586.png)

新建一个文件夹，命名最好英文，这里命名为`blog`，在该文件夹内右键打开 `Git Bash` ，输入命令安装：

```
npm install hexo-cli -g
```

安装完后使用 `hexo -v` 查看版本，验证安装是否完成

![image-20230719215441428](image-20230719215441428.png)

初始化hexo，输入命令创建文件夹`myblog`（也可以根据习惯修改文件夹名），这个文件夹就是<mark>站点根目录</mark>，后面会多次提到站点根目录

```
hexo init myblog
```

然后输入命令进入`myblog`文件夹：

```
cd myblog
```

输入：

```
npm install
```

![image-20230719220502367](image-20230719220502367.png)

再依次输入：（也可输入简写：`hexo g` 和 `hexo s`）

```
hexo generate
hexo server
```

`hexo generate` 顾名思义，生成静态文章，可以用 `hexo g`缩写
`hexo server` 在本地开启服务，可以用`hexo s`缩写。后续修改配置会经常使用这个命令在本地查看效果。

![image-20230719220908793](image-20230719220908793.png)

根据命令行最后一行的提示`Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop`，可以在浏览器输入 `http://localhost:4000/`，就可以在本地看到博客效果了。在`Git Bash`中按`Ctrl+C`退出服务。

![image-20230719221213383](image-20230719221213383.png)

到这里博客就已经生成好了。



# 5、免费部署到GitHub

在GitHub中新建仓库

![image-20230719221649324](image-20230719221649324.png)

创建一个仓库，命名为 `你的用户名.github.io`，只有这样，将来要部署到GitHub page的时候，才会被识别，也就是xxxx.github.io，其中xxx就是你注册GitHub的用户名。点击底部的`Create repository`创建。

![image-20230719221838539](image-20230719221838539.png)

在`Git Bash`中输入以下两条，检查之前的用户名和邮箱输对没有：

```
git config user.name
git config user.email
```

然后创建SSH，<mark>输入指令后需要按几次回车</mark>

```
ssh-keygen -t rsa -C "输入你的邮箱"
```

![image-20230719222606342](image-20230719222606342.png)

这个时候它会告诉你已经生成了.ssh的文件夹。在你的电脑中找到这个文件夹。

![image-20230719222836726](image-20230719222836726.png)

> ssh，简单来讲，就是一个秘钥，其中，id_rsa是你这台电脑的私人秘钥，不能给别人看的，id_rsa.pub是公共秘钥，可以随便给别人看。把这个公钥放在GitHub上，这样当你链接GitHub自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过git上传你的文件到GitHub上。

在GitHub的`setting`中，找到`SSH keys`的设置选项，点击`New SSH key`

把你的`id_rsa.pub`（可以用记事本打开）里面的信息复制到key。点击`Add SSH key`

![image-20230719223321141](image-20230719223321141.png)

在`Git Bash`中，查看是否成功（中间要输入一次yes），最后出现successfully字样就是成功了。

```
ssh -T git@github.com
```

![image-20230719223736052](image-20230719223736052.png)

这一步，我们就可以将hexo和GitHub关联起来，也就是将hexo生成的文章部署到GitHub上，打开站点配置文件 `_config.yml`，翻到最后，修改为：

```
deploy:
  type: git
  repo: https://github.com/你的GitHub名字/你的GitHub名字.github.io.git
  branch: master
```

![image-20230719224127052](image-20230719224127052.png)

这个时候需要先安装deploy-git ，也就是部署的命令，这样你才能用命令部署到GitHub。在`Git Bash`中：

```
npm install hexo-deployer-git --save
```

![image-20230719224402356](image-20230719224402356.png)

然后依次输入：（输入`hexo d`可能出问题，大多是网络问题，可以多试几次，或过一会再试）

（一直出问题可以参考：[Hexo d部署报错之spawn failed的解决方案](https://blog.csdn.net/Kevin_Carpricron/article/details/124069885) 的方法2）

```
hexo clean
hexo g
hexo d
```

其中 `hexo clean`清除了你之前生成的东西，也可以不加。

`hexo deploy` 部署文章，可以用`hexo d`缩写

`hexo d` 过程中会提示登录GitHub

![image-20230719224938980](image-20230719224938980.png)

部署成功后就可以在浏览器输入：`https://用户名.github.io/`看到博客了。（部署后一般需要等几分钟）
