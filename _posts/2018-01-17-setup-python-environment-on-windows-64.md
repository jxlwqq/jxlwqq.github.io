---
layout: post
title: "Windows 64 位系统下 Python 环境的搭建"
date: 2018-01-17 18:03:00 +0800
categories: python windows
---

## Windows 64 位开发环境

> 注意：本教程适用于 Windows 7 64 位操作系统 及 Windows 10 64 位操作系统，其他系统尚未经过校验。

#### 安装 IDE

PyCharm 下载：<https://www.jetbrains.com/pycharm/>

#### 安装 Python 环境

Python2.7 下载：<https://www.python.org/downloads/>

Python2.7 的默认安装目录在 `C:/Python27/`，**安装目录请勿转移到其他盘！有C盘洁癖症的患者请特别留意！**。

#### 将 Python 加入环境变量

```
C:\Python27;
C:\Python27\Scripts;
```

将上述两个路径加入系统环境变量中。

> 在`我的电脑`右键属性----》点击左侧列表中的高级系统设置-----》高级分页下，点击下面的环境变量-----》在系统变量选框中，找到并选择变量名为 Path 的变量，选择后点击下面的编辑按钮，最后在弹出来的系统变量编辑对话框中的变量值的最前（或最后）加上`C:\Python27;C:\Python27\Scripts;` （注意后面还有个分号，不要漏掉分号的，分号的作用是用来间隔变量与变量的。）

#### 将 Python2.7 添入 Windows 系统的注册表

新建文件 `register.py` 并写入：

```python
import sys
from _winreg import *
version = sys.version[:3]
installpath = sys.prefix
regpath = "SOFTWARE\\Python\\Pythoncore\\%s\\" % (version)
installkey = "InstallPath"
pythonkey = "PythonPath"
pythonpath = "%s;%s\\Lib\\;%s\\DLLs\\" % (
    installpath, installpath, installpath
)
def RegisterPy():
    try:
        reg = OpenKey(HKEY_CURRENT_USER, regpath)
    except EnvironmentError as e:
        try:
            reg = CreateKey(HKEY_CURRENT_USER, regpath)
            SetValue(reg, installkey, REG_SZ, installpath)
            SetValue(reg, pythonkey, REG_SZ, pythonpath)
            CloseKey(reg)
        except:
            print "*** Unable to register!"
            return
        print "--- Python", version, "is now registered!"
        return
    if (QueryValue(reg, installkey) == installpath and
        QueryValue(reg, pythonkey) == pythonpath):
        CloseKey(reg)
        print "=== Python", version, "is already registered!"
        return
    CloseKey(reg)
    print "*** Unable to register!"
    print "*** You probably have another Python installation!"
if __name__ == "__main__":
    RegisterPy()
```

进入 register.py 所在目录后，执行：

```
python register.py
```

#### 安装 pywin32

pywin32 下载：[https://nchc.dl.sourceforge.net/project/pywin32/pywin32/Build 219/pywin32-219.win-amd64-py2.7.exe](https://nchc.dl.sourceforge.net/project/pywin32/pywin32/Build%20219/pywin32-219.win-amd64-py2.7.exe)

#### 安装 VCForPython27

VCForPython27 下载：<https://download.microsoft.com/download/7/9/6/796EF2E4-801B-4FC4-AB28-B59FBF6D907B/VCForPython27.msi>

#### 安装并升级 pip

##### 安装 pip

下载 get-pip.py 文件：<https://bootstrap.pypa.io/get-pip.py>

进入 get-pip.py 所在目录后，执行：

```
python get-pip.py
```

##### 升级 pip

```
python -m pip install -U pip
```

#### 安装 lxml

有些同学可能会有疑问，说直接用 `pip install lxml` 安装不就行了吗？反正我试了几次都不行。还是老老实实地下载 whl 文件，然后在本地安装吧。这么说吧，如果你通过在线安装遇到问题的，都可以通过本地安装的方式解决问题。  
推荐一个下载网站：<https://www.lfd.uci.edu/~gohlke/pythonlibs/>  
上面有常用的 Python 类库。

lxml 下载：<https://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml>

找到对应的版本下载，然后进入 lxml 的下载目录，执行：

```
pip install lxml‑4.1.1‑cp27‑cp27m‑win_amd64.whl
```

#### 安装 MySQL-Python

同理，MySQL-Python 下载：<https://www.lfd.uci.edu/~gohlke/pythonlibs/#mysql-python>

进入 MySQL-Python 的下载目录，执行：

```
pip install MySQL_python‑1.2.5‑cp27‑none‑win_amd64.whl
```

#### 安装 Scrapy 爬虫框架

```
pip install Scrapy
```

#### 安装 Flask Web 框架

```
pip install flask
```

#### 最后的话

说实话，Windows 平台并不适合某些语言的开发，尤其是 Web 方向的。能用 MacOS 或者 Linux 的还是别用 Windows 了。为什么有这篇文章呢，还不是为了给用 Windows 的同事配环境？说多了都是泪。
