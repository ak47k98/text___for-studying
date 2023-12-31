（基于狗屎教程）：

## 关于下载失败（卡在20%）

建议先配置好.ssh使用.ssh可以实现稳定下载：

git clone https://github.com/ArduPilot/ardupilot 

  =====>   git clone git@github.com:ArduPilot/ardupilot.git

配置.ssh教程见：[3.5git 与 github | HDU-CS-WIKI (xyxsw.site)](https://wiki.xyxsw.site/3.编程思维体系构建/3.5git与github)

（同时还有git的命令）

配置时在ubuntu系统中建议cd 到.ssh文件夹中直接./id_rsa.pub打开读取秘钥。

## 关于公钥报错：

警告表示`apt-key`已被弃用，并建议使用`trusted.gpg.d`目录中的密钥环文件进行管理，这是更现代的替代方法。在你的情况下，导入密钥的命令为：

```
bashCopy code
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
```

为了适应新的方法，你可以按照以下步骤进行操作：

1. **创建 GPG 密钥环文件：**

   ```
   bashCopy codegpg --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
   gpg --export --armor 3B4FE6ACC0B21F32 | sudo tee /usr/share/keyrings/ubuntu-archive-keyring.gpg
   ```

   这将从密钥服务器下载密钥并将其导出到一个GPG密钥环文件中。

2. **更新源列表：**

   编辑你的 `/etc/apt/sources.list` 文件，包含GPG密钥文件：

   ```
   bashCopy code
   deb [signed-by=/usr/share/keyrings/ubuntu-archive-keyring.gpg] http://mirrors.aliyun.com/ubuntu bionic main
   ```

   根据需要调整路径，并确保它匹配你创建的密钥环文件。

   细节：

   请按照以下步骤操作：

   使用文本编辑器打开 `/etc/apt/sources.list` 文件。你可以使用 `nano` 或 `gedit`：

   使用 `nano`：

   ```
   bashCopy code
   sudo nano /etc/apt/sources.list
   ```

   或者使用 `gedit`：

   ```
   bashCopy code
   sudo gedit /etc/apt/sources.list
   ```

   在文件中找到类似于以下行的条目：

   ```
   bashCopy code
   deb http://mirrors.aliyun.com/ubuntu bionic main
   ```

   1. 将其修改为：

   ```
   bashCopy code
   deb [signed-by=/usr/share/keyrings/ubuntu-archive-keyring.gpg] http://mirrors.aliyun.com/ubuntu bionic main
   ```

   ​    保存并关闭编辑器。

   # **更新并重新运行安装脚本：**
   运行以下命令来更新你的软件包列表并重新运行安装脚本：

   ```
   bashCopy codesudo apt-get update
   ./install-prereqs-ubuntu.sh -y
   ```

这些步骤应该解决弃用警告，并帮助你以符合 Ubuntu 推荐的现代实践方式导入 GPG 密钥。



#      ***网络问题***   ！！！！！！！

##     在执行时发现克隆错误报错

1.![屏幕截图 2023-12-31 114010](D:\c s studying\text___for-studying\SITL\屏幕截图 2023-12-31 114010.png)

2.换个网络重试（校园网换热点）（或者换张卡的流量）（祈祷宿舍出奇迹）

3.clash for linux

4.手动下载 cd到报错文件夹 手动git clone 建议是找到仓库后用.ssh下，成功率高。

5.在Windows上下好后拷贝到Ubuntu上



# 教程的补漏

1.git submodule update --init --recursive 这一步后检查报错 可能会少文件（出现空文件夹）执行上节4的指令。

（高概率是：ChibiOS库缺失）

2.Tools/environment_install/install-prereqs-ubuntu.sh-y

. ~/.profile

替换为：Tools/environment_install/install-prereqs-ubuntu.sh -y

. ~/.profile

同时：高概率出现网络错误，也要检查报错，而且容易卡（换个网吧悲）

![截图 2023-12-30 15-57-49](D:\c s studying\text___for-studying\SITL\截图 2023-12-30 15-57-49.png)

3.如果中途解压报错，建议直接全部重来。（无慈悲）

![截图 2023-12-30 18-22-31](D:\c s studying\text___for-studying\SITL\截图 2023-12-30 18-22-31.png)(这样算搞定)

4.执行  sim_vehicle.py -w 时注意waf库的缺失问题（可能要手动补）

![截图 2023-12-30 18-58-09](D:\c s studying\text___for-studying\SITL\截图 2023-12-30 18-58-09.png)![截图 2023-12-30 18-59-14](D:\c s studying\text___for-studying\SITL\截图 2023-12-30 18-59-14.png)

5.sudo -H pip2 install --upgrade MAVProxy pymavlink future lxml   ====>>>>   sudo -H pip install --upgrade MAVProxy pymavlink future lxml

6.执行  sim_vehicle.py 时只出现一个窗口 ：![截图 2023-12-30 21-59-05](D:\c s studying\text___for-studying\SITL\截图 2023-12-30 21-59-05.png)

这是要注意报错 :Failed to load module: No module named 'console'. Use 'set moddebug 3' in the MAVProxy console to enable traceback Failed to load module: No module named 'map'. Use 'set moddebug 3' in the MAVProxy console to enable traceback

**在命令提示符中输入mavproxy.py进入控制台。输入module load map 而不是报错中的   set moddebug 3**     

会输出报错：MAV> module load map MAV> No module named **'wx'** Traceback (most recent call last):  File "/home/ak47k98/.local/bin/mavproxy.py", line 374, in load_module    module = m.init(mpstate, **kwargs)             ^^^^^^^^^^^^^^^^^^^^^^^^^  File "/home/ak47k98/.local/lib/python3.11/site-packages/MAVProxy/modules/mavproxy_map/__init__.py", line 1111, in init    return MapModule(mpstate)           ^^^^^^^^^^^^^^^^^^  File "/home/ak47k98/.local/lib/python3.11/site-packages/MAVProxy/modules/mavproxy_map/__init__.py", line 68, in __init__    from MAVProxy.modules.mavproxy_map import mp_slipmap  File "/home/ak47k98/.local/lib/python3.11/site-packages/MAVProxy/modules/mavproxy_map/mp_slipmap.py", line 19, in <module>    from MAVProxy.modules.lib import win_layout  File "/home/ak47k98/.local/lib/python3.11/site-packages/MAVProxy/modules/lib/win_layout.py", line 4, in <module>    import os, wx, pickle ModuleNotFoundError: No module named 'wx' No module named 'map' Traceback (most recent call last):  File "/home/ak47k98/.local/bin/mavproxy.py", line 689, in import_package    mod = __import__(name)          ^^^^^^^^^^^^^^^^ ModuleNotFoundError: No module named 'map' During handling of the above exception, another exception occurred:

answer from GPT ：

看起来 `MAVProxy` 提示缺少 `wx` 模块，这是一个 GUI 库，用于创建图形用户界面。在使用 `MAVProxy` 的 `map` 模块时，它尝试引入 `wx` 模块，但由于缺少，导致了错误。

要解决这个问题，你可以尝试安装 `wxPython`，这是 `wx` 模块的 Python 绑定。你可以使用以下命令来安装：

```
bashCopy code
pip install -U wxPython
```

这将安装 `wxPython`，并希望解决缺少 `wx` 模块的问题。然后，你可以再次尝试加载 `map` 模块：

```
bashCopy code
module load map
```

如果安装 `wxPython` 之后仍然存在问题，请确保你的 Python 版本与 `wxPython` 兼容。有时，特定版本的库可能需要特定版本的 Python。

如果问题仍然存在，你可以尝试检查 `MAVProxy` 和 `wxPython` 的版本兼容性，并相应地调整它们。

接下来由于安装了虚拟环境会导致报错：

MAV> module load map MAV> /lib/x86_64-linux-gnu/libgio-2.0.so.0: undefined symbol: g_log_set_debug_enabled Traceback (most recent call last):  File "/home/ak47k98/.local/bin/mavproxy.py", line 374, in load_module    module = m.init(mpstate, **kwargs)             ^^^^^^^^^^^^^^^^^^^^^^^^^  File "/home/ak47k98/.local/lib/python3.11/site-packages/MAVProxy/modules/mavproxy_map/__init__.py", line 1111, in init    return MapModule(mpstate)           ^^^^^^^^^^^^^^^^^^  File "/home/ak47k98/.local/lib/python3.11/site-packages/MAVProxy/modules/mavproxy_map/__init__.py", line 68, in __init__    from MAVProxy.modules.mavproxy_map import mp_slipmap  File "/home/ak47k98/.local/lib/python3.11/site-packages/MAVProxy/modules/mavproxy_map/mp_slipmap.py", line 19, in <module>    from MAVProxy.modules.lib import win_layout  File "/home/ak47k98/.local/lib/python3.11/site-packages/MAVProxy/modules/lib/win_layout.py", line 4, in <module>    import os, wx, pickle  File "/home/ak47k98/anaconda3/lib/python3.11/site-packages/wx/__init__.py", line 17, in <module>    from wx.core import *  File "/home/ak47k98/anaconda3/lib/python3.11/site-packages/wx/core.py", line 12, in <module>    from ._core import * ImportError: /lib/x86_64-linux-gnu/libgio-2.0.so.0: undefined symbol: g_log_set_debug_enabled No module named 'map' Traceback (most recent call last):  File "/home/ak47k98/.local/bin/mavproxy.py", line 689, in import_package    mod = __import__(name)          ^^^^^^^^^^^^^^^^ ModuleNotFoundError: No module named 'map' During handling of the above exception, another exception occurred: Traceback (most recent call last):  File "/home/ak47k98/.local/bin/mavproxy.py", line 372, in load_module    m = import_package(modpath)        ^^^^^^^^^^^^^^^^^^^^^^^  File "/home/ak47k98/.local/bin/mavproxy.py", line 692, in import_package    mod = __import__(name)          ^^^^^^^^^^^^^^^^ ModuleNotFoundError: No module named 'map' Failed to load module: No module named 'map'.

看起来这个问题可能与 `libgio-2.0.so.0` 这个库的 undefined symbol 有关。这可能是由于不同库版本之间的冲突或不兼容性引起的。

你可以尝试在 Anaconda 环境外运行 `MAVProxy`，以确保它使用系统的库而不是 Anaconda 中的库。你可以通过激活你的 Anaconda 环境，然后禁用 Anaconda 的环境变量，再运行 `MAVProxy`，例如：

```
bashCopy codeconda deactivate  # 禁用 Anaconda 环境
MAVProxy
```

基本上可以实现安装，可以成功打开页面力![截图 2023-12-30 21-59-02](D:\c s studying\text___for-studying\SITL\截图 2023-12-30 21-59-02.png)![截图 2023-12-30 21-54-32](D:\c s studying\text___for-studying\SITL\截图 2023-12-30 21-54-32.png)
