# #Anaconda 使用文档

Windows在开始菜单中打开“Anaconda Prompt”，MacOS和Linux打开“Terminal”（“终端”）进行操作。

## #Anaconda安装更新

### #验证Anaconda是否安装成功
```cmd
* conda --version
```
终端上将会以` conda 版本号 `的形式显示当前安装conda的版本号。如：`conda 3.11.0`  表示安装成功

### #更新conda到最新版本
```cmd
* conda update conda #升级conda到最新版本
* conda update anaconda #升级anaconda到最新版本
```

### #查看conda帮助信息
```cmd
* conda --help
* conda -h
```

## #环境管理

### #创建新环境

```cmd
* conda create --name <env_name> <package_names>
* conda create -n <env_name> <package_names>
```

* `<env_name>` 即创建的环境名称。
* `<package_names>` 即安装在环境中的包名。
     * 如果要安装指定的版本号，则只需要在包名后面以=和版本号的形式执行。如：`conda create --name python2 python=2.7`，即创建一个名为“python2”的环境，环境中安装版本为2.7的python。
    * 如果要在新创建的环境中创建多个包，则直接在<package_names>后以空格隔开，添加多个包名即可。如：`conda create -n python3 python=3.5 numpy pandas`，即创建一个名为“python3”的环境，环境中安装版本为3.5的python，同时也安装了numpy和pandas。
* `--name` 可以使用`-n`替换

### #切换环境
```cmd
* source activate <env_name>    #Linux or macos
* activate <env_name>   #Windows
```

* 如果创建环境后安装Python时没有指定Python的版本，那么将会安装与Anaconda版本相同的Python版本，即如果安装Anaconda第2版，则会自动安装Python 2.x；如果安装Anaconda第3版，则会自动安装Python 3.x
* 当成功切换环境之后，在该行行首将以`(env_name)`或`[env_name]`开头。其中，`env_name`为切换到的环境名。如：在macOS系统中执行`source active python2`，即切换至名为“python2”的环境，则行首将会以`(python2)`开头

### #退出Anaconda环境

1. Linux Or MacOS
```cmd
* source deactivate
```

2. Windows
```cmd
* deactivate
```

3. 退出当前环境，行首以`(env_name)`或`[env_name]`开头的字符将不再显示

### #显示已创建环境
```cmd
* conda info --envs
* conda info -e
* conda nev list
```

* 如执行`aconda env list`结果：
```
(base) C:\Users\vshzh>conda env list
# conda environments:
#
base                  *  D:\Development\Anaconda3
py3                      D:\Development\Anaconda3\envs\py3
```
结果中星号“*”所在行，即为当前所在的环境。默认(base)

### #复制环境
```cmd
* conda create --name <new_env_name> --clone <copied_nev_name>
```

* `<copied_env_name>`即为被复制或克隆的环境名
* `<new_env_name>`即为复制后新环境名称
* `conda create --name py2 --clone python2` #通过clone得到一个新的与python2相同配置的环境py2

### #删除环境
```cmd
* conda remove --name <env_name> --all #删除创建环境所有配置
```

## #package(包)管理

### 1.查找可供安装的package版本

1. 精确查找
```cmd
* conda search --full-name <package_full_name>
```
* `--full-name`为精确查找的参数
* `<package_full_name>`被查找包的全名

2. 模糊查找
```cmd
* conda search <text>
```
* `<text>`是查找的package(包)名中包含的字段

### 2.获取当前环境中已安装的包信息
```cmd
* conda list 
```
* 显示当前环境已安装包的名称及版本号

### 3.安装包
1. 指定环境安装
```cmd
* conda install --name <env_name> <package_name>
```
* `<env_name>` 包安装指定的环境；`<package_name>` 需要安装的包名

2. 在当前环境中安装包
```cmd
* conda install <package_name>
```
* `<package_name>` 需要安装的包名，在当前环境中安装

### 4.卸载包
1. 卸载指定环境的包
```cmd
* conda remove --name <env_name> <package_name>
```
* `<`env_name>` 卸载包所在环境名称
* `<package_name>` 需要卸载包的名称
* 如：conda remove -name python2 pandas

2. 卸载当前环境中的包
```cmd
* conda remove <package_name>
```
* `<package_name>` 需要卸载包的名称
* 执行命令后即在当前环境中移除指定的包

### 5.更新包
1. 更新所有包
```cmd
* conda update --all
* conda upgrade --all
```

2. 更新指定包
```cmd
* conda update <package_name>
* conda upgrade <package_name>
```

* `<package_name>` 为指定更新的包名
* 更新多个指定包时。多个包名以空格分割

## #设置镜像
如果需要安装很多packages，你会发现conda下载的速度经常很慢，因为Anaconda.org的服务器在国外。所幸的是，清华TUNA镜像源有Anaconda仓库的镜像，我们将其加入conda的配置即可：

```cmd
# 添加Anaconda的TUNA镜像
* conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
# TUNA的help中镜像地址加有引号，需要去掉
 
# 设置搜索时显示通道地址
* conda config --set show_channel_urls yes
```

执行完上述命令后，会生成~/.condarc(Linux/Mac)或C:UsersUSER_NAME.condarc文件，记录着我们对conda的配置，直接手动创建、编辑该文件是相同的效果
