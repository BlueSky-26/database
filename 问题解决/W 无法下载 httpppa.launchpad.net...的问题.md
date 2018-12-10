## W: 无法下载 http://ppa.launchpad.net/***/...的问题

执行apt-get update时出现以下情况

W: 无法下载 http://ppa.launchpad.net/fcitx-team/nightly/ubuntu/dists/jessie/main/binary-amd64/Packages  404  Not Found

解决办法：将对应的PPA删除掉即可

使用以下命令切换到对应PPA目录：

cd /etc/apt/sources.list.d

例如：
W: 无法下载 http://ppa.launchpad.net/wine/wine-builds/ubuntu/dists/bionic/InRelease  无法连接上 ppa.launchpad.net:80 (91.189.95.83)，连接超时
W: 部分索引文件下载失败。如果忽略它们，那将转而使用旧的索引文件。



找到上述无法下载的对应PPA目录，即wine-ubuntu-wine-builds-bionic.list，安全起见，用mv命令将该文件添加后缀.bak即可