# 基于Anaconda的Python开发环境搭建

## 特点

Anaconda是包管理器和环境管理器，自带了多个Python包，且可以创建多个Python环境，

Jupyter可以将数据分析的代码、图像和文档全部组合到一个web文档中

VS-Code是一个依靠插件的编辑器

## 安装Anaconda

### Anaconda特点

> 参考知乎文章：[自学Anaconda的正确姿势](https://www.zhihu.com/question/58033789/answer/254673663)



1. Anaconda 附带了一大批常用数据科学包，它附带了 conda、Python 和 150 多个科学包及其依赖项。因此你可以立即开始处理数据。

2. 包管理器conda

Anaconda 是在 conda（一个包管理器和环境管理器）上发展出来的。

在数据分析中，你会用到很多第三方的包，而conda（包管理器）可以很好的帮助你在计算机上安装和管理这些包，包括安装、卸载和更新包。

3. 创建和管理环境

为什么需要管理环境呢？

比如你在A项目中用了 Python 2，而新的项目B老大要求使用Python 3，而同时安装两个Python版本可能会造成许多混乱和错误。这时候 conda就可以帮助你为不同的项目建立不同的运行环境。

还有很多项目使用的包版本不同，比如不同的pandas版本，不可能同时安装两个 Numpy 版本，你要做的应该是，为每个 Numpy 版本创建一个环境，然后项目的对应环境中工作。这时候conda就可以帮你做到。



### 安装步骤

[官网下载](https://www.anaconda.com/products/individual#windows)，按照步骤安装即可。

Anaconda 的下载文件比较大（约 500 MB），因为它附带了 Python 中最常用的数据科学包。

如果计算机上已经安装了 Python，安装不会对你有任何影响。实际上，脚本和程序使用的默认 Python 是 Anaconda 附带的 Python，**所以安装完Anaconda已经自带安装好了Python，不需要你再安装Python了。**

**注意：如果你是windows 10系统，注意在安装Anaconda软件的时候，右击安装软件→选择以管理员的身份运行。**



### 界面操作

#### Anaconda Navigator

所有的图形界面操作都需要在Anaconda Navigator中操作

#### Home

用于选择已创建的环境，启动安装的程序，在这个界面启动的程序自动运行在已选择的环境上，比如`base(root)`环境

此界面包含了`VS Code`, `Jupyter notebook`, `CMD Prompt`, `Spyder`等程序

#### Environments

用于具体操作环境：创建、删除、管理环境中的包等 

#### Learning

包含很多官方和社区的学习内容



### 命令行操作

Anaconda自带了CMD，但是每次启动一个窗口太过麻烦，最好的情况是将`Command line`、`Editor`、`Jupyter notebook`集成到 `VS Code`中

#### conda命令

1. `conda --version` #查看conda版本，验证是否安装

2. `conda update conda` #更新至最新版本，也会更新其它相关包

3. `conda update --all` #更新所有包

4. `conda update package_name` #更新指定的包

5. `conda create -n env_name package_name` #创建名为env_name的新环境，并在该环境下安装名为package_name 的包，可以指定新环境的版本号，例如：conda create -n python2 python=python2.7 numpy pandas，创建了python2环境，python版本为2.7，同时还安装了numpy pandas包

6. `conda activate env_nam`e #**切换/激活环境**至env_name环境

7. `conda deactivate` #**退出环境**

8. `conda info -e` #显示所有已经创建的环境

9. `conda create --name new_env_name --clone old_env_name` #**复制环境**old_env_name为new_env_name

10. `conda remove --name env_name –all` #删除环境

11. `conda list` #**查看所有已经安装的包**

12. `conda install package_name` #**在当前环境中安装包**

13. `conda install --name env_name package_name` #在指定环境中安装包

14. `conda remove -- name env_name package` #删除指定环境中的包

15. `conda remove package` #删除当前环境中的包

16. `conda create -n tensorflow_env tensorflow`

conda activate tensorflow_env #conda 安装tensorflow的CPU版本

17. conda create -n tensorflow_gpuenv tensorflow-gpu

conda activate tensorflow_gpuenv #conda安装tensorflow的GPU版本

18. conda env remove -n env_name #采用第10条的方法删除环境失败时，可采用这种方法



#### powershell激活

默认情况下，win10自带的powershell无法使用`conda activate`命令激活已经创建的环境

对于conda > 4.6的情况，解决方法如下：

- 用Win + X 组合键调出PowerShell 管理员模式；

- 执行命令

  ```powershell
  conda init powershell
  ```

  关闭当前powershell窗口，重新打开一个powershell窗口输入`conda activate 环境名`测试。

CMD 的话只需把上面三步中的powershell 改为cmd.exe 即可。

完成上述步骤后，启动powershell会自动进入`base(root)`环境，如果不想启动进入环境，则执行：

```powershell
conda config --set auto_activate_base false
```

同样，如果想启动即进入，则执行：

```powershell
conda config --set auto_activate_base true
```



#### Jupyter notebook使用

Jupyter notebook已经是科学分析的常用工具，特点是可以保留分析过程。

##### 功能介绍

Jupyter中代码可以分块执行，且可以查看和留中间输出变量，将数据分析过程变得直观易懂。

VScode目前已经原生支持Jupyter notebook，通过调出命令，选择`Jupyter: Create new Jupyter notebook`即可。

或者先新建`.ipynb`文件，再用vscode打开

```
ni test.ipynb -type file  //win10
touch test.ipynb          //Linux

code test.ipynb
```

##### 安装内核

对于`conda`建立的虚拟环境，需要安装jupyter的内核`ipykernel`才能被jupyter文件连接到环境

##### 导出为PDF

目前VS Code中已经集成了jupyter notebook的基本功能，但是每次打开需要`.ipynb`文件需要时间，且万一改动，之前的过程可能不复存在，最好是可以导出为PDF供后续参考。web版的Jupyter notebook可以导出多种格式，不方便之处是需要打开网页版。VS Code版可以导出为`PDF`,`HTML`格式，但是需要安装插件。

直接导出会失败，提示缺少xelatex：

1. [下载MiKTex](https://miktex.org/download)，根据提示逐步安装
2. 打开VS code，将一个`.ipynb`文件导出为PDF，根据提示安装`.sty`文件
3. `.sty`文件有一大堆，耐心逐个点击`Install`
4. 工作完成后即可丝滑导出为PDF，其中Markdown的各级标题会显示为目录















