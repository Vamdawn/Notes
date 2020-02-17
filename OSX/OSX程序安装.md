## OSX下应用程序安装的几种情况

#### 移动程序

挂载dmg或者下载得到应用程序，**移动或者拷贝到【应用程序】目录**。

#### 安装程序

挂载dmg或者下载得到安装程序，**双击打开进行安装**。

*注：此情况下，双击打开安装程序 = 运行安装程序包内容下的一个可执行文件。*

*路径为：`Installer.app/Contents/MacOS/excutable_file`*

*特殊情况安装程序需要root权限时，可以使用root命令执行该文件：*

```shell
sudo path/Installer.app/Contents/MacOS/excutable_file
# INPUT PASSWORD
```

