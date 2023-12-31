https://blog.csdn.net/weixin_43912621/article/details/132649944
https://blog.csdn.net/weixin_43507693/article/details/109015177





Anaconda是一个开源的Python和R编程语言的发行版本，它包含了很多用于科学计算、数据分析和机器学习的工具和库。Anaconda提供了一个方便的工具来创建和管理虚拟环境，使得你可以在不同项目中使用不同版本的库和工具，以防止冲突。以下是在Anaconda中创建和使用虚拟环境的基本步骤：

检查版本号：conda --version 
1. 安装Anaconda
首先，确保你已经安装了Anaconda。你可以从Anaconda官方网站（https://www.anaconda.com/products/individual）下载适合你操作系统的安装包，并按照官方文档中的说明进行安装。

2. 打开Anaconda Navigator或使用命令行
你可以使用Anaconda Navigator图形界面，也可以使用命令行进行操作。下面分别介绍两种方式。

使用Anaconda Navigator：
打开Anaconda Navigator应用程序。
在Navigator界面中，选择"Environments"选项卡。
点击"Create"按钮创建一个新的虚拟环境。
输入虚拟环境的名称，选择Python版本，然后点击"Create"按钮。
使用命令行：
打开命令行终端。
**创建一个新的虚拟环境，例如：**
**bash**
**Copy code**
**conda create --name myenv python=3.8**
**这里myenv是你给虚拟环境取的名字，python=3.8表示使用Python 3.8版本。**

3. 激活虚拟环境
使用Anaconda Navigator：
在"Environments"选项卡中，找到你创建的虚拟环境，点击右侧的"Play"按钮来激活它。
使用命令行：
**在命令行中输入以下命令激活虚拟环境：**
**bash**
**Copy code**
**conda activate myenv**
**这里的myenv是你创建的虚拟环境的名称。**
4. 安装和管理包
在激活的虚拟环境中，你可以使用conda install命令安装需要的Python包，例如：

bash
Copy code
conda install numpy pandas matplotlib
5. 退出虚拟环境
**无论是在Anaconda Navigator中还是命令行中，都可以使用以下命令退出虚拟环境：**

**bash**
**Copy code**
**conda deactivate**
通过这些步骤，你就可以在Anaconda中创建、激活和管理虚拟环境了，以便更好地组织和隔离不同项目的依赖关系。




从你提供的输出来看，你当前处于Anaconda的base环境中。在这个环境中，你可以执行Python和conda命令。如果你想创建一个新的虚拟环境或切换到已有的虚拟环境，你可以按照上面提到的步骤进行操作。

如果你想创建一个新的虚拟环境，可以使用以下命令：

bash
Copy code
conda create --name myenv python=3.8
然后，激活新创建的环境：

bash
Copy code
conda activate myenv
在激活的环境中，你可以安装所需的Python包，并进行其他项目特定的配置。

**如果你想查看当前存在的所有虚拟环境，可以使用以下命令：**

**bash**
**Copy code**
**conda env list**
如果你想退出当前虚拟环境，可以运行：

bash
Copy code
conda deactivate
请注意，当你不再需要使用Anaconda时，你可以直接关闭终端或退出Anaconda Navigator。







从你的输出中可以看到，你正在创建一个名为python3.8的虚拟环境，并安装了Python 3.8以及相关的一些包。在这里，你需要执行以下步骤来激活和使用这个虚拟环境：

激活虚拟环境：

bash
Copy code
conda activate python3.8
这样你就会进入到新创建的python3.8虚拟环境。

使用虚拟环境：

在激活的虚拟环境中，你可以安装其他Python包，运行你的项目等。

退出虚拟环境：

当你完成工作或者需要切换到其他环境时，可以执行以下命令退出当前虚拟环境：

bash
Copy code
conda deactivate
请注意，在你需要使用虚拟环境时，始终记得激活它；在不需要时，记得退出以避免可能的包冲突。




2.2 使用清华镜像源网站
切换到国内的镜像源（为什么要切换原因就不用多说了吧（手动狗头））
分别输入以下4行代码：

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/


conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/

这个配置好以后，以后再安装其他的软件如果要用到清华镜像源网站就不用了重新配置了。

注意！如果切换镜像后当出现下载不了的情况，就先切换默认源，然后再修改另一个可以使用的conda源（一定要先恢复默认，再换另一个！！！）
切回默认源：

conda config --remove-key channels


————————————————
版权声明：本文为CSDN博主「伏城无嗔」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_45281807/article/details/112442423



安装成功后，输入以下指令：conda info --envs
即可看到 conda 环境中，有新建的 pytorch 环境，右边的 * 号表示，当前你处于哪个环境。





这段输出表明您已经成功安装了scikit-learn，并且您可以使用scikit-learn-intelex来加速它。scikit-learn-intelex是一个由英特尔开发的加速器，可以提高scikit-learn在英特尔处理器上的性能。

要使用scikit-learn-intelex，您可以运行以下命令来安装它：

conda install scikit-learn-intelex
然后，您可以使用以下命令来加速您的应用程序：

python -m sklearnex my_application.py



输入：conda --version检查版本号。（Anaconda）
：# 打开终端或命令提示符

# 进入 Python 交互式环境
python

# 在 Python 交互式环境中导入 PyTorch 并打印版本
>>> import torch
>>> print(torch.__version__)

# 退出 Python 交互式环境（如果需要）
>>> exit()