（基于教程）

## 关于下载失败（卡在20%）

建议先配置好.ssh使用.ssh可以实现稳定下载：

git clone https://github.com/ArduPilot/ardupilot 

  =====>   git clone git@github.com:ArduPilot/ardupilot.git

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
