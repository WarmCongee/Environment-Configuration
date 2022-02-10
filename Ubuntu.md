ubuntu重装

# Protobuf

安装各版本通用，ubuntu下建议./configure --prefix=/usr安装在usr目录下。默认会安装在/usr/local，用cmake编译找包时容易找不到

https://github.com/protocolbuffers/protobuf/blob/master/src/README.md

# g++/gcc

直接apt安装卸载，可以多版本共存。

可以切换优先级和默认版本

```shell
sudo update-alternatives --install /usr/local/bin/gcc gcc /usr/local/bin/gcc-11 10
sudo update-alternatives --install /usr/local/bin/g++ g++ /usr/local/bin/g++-11 10
sudo update-alternatives --config g++
```

https://blog.csdn.net/iRiven/article/details/114435544

# python

系统python同上

注意/user/include下的python头文件资源，并不在apt包如python3.9的包中，而是在python3.9-dev这个包中。

所有的第三方包annaconda虚拟环境配置

# Clion Config

不加设置会使用clion默认的cmake，make，c编译器，c++编译器

可以自选，一般都在/usr/bin路径下

修改c编译器，c++编译器，会调整调用/usr/include目录下不同c++版本的头文件

修改make，会调整调用/usr/include目录下不同其他库如Python.h头文件

/usr目录下的库和资源都可以被cmake和编译器找到，/usr/local下的记得额外设置系统环境变量或者别的

# gnome拓展

如果通过浏览器拓展设置本地gnome拓展有问题，手动增加gnome拓展。将插件包移动到

/home/warmcongee/.local/share/gnome-shell/extensions目录下，同时文件夹名称与包内metadata.json的uuid值相同

# gnome主题

主题放置在/home/warmcongee/.local/share/themes目录下，gnome的主题插件会自动搜索到

图标风格放在/home/warmcongee/.local/share/icons目录下

# Docker

一次性使用的环境能用docker就别自己配