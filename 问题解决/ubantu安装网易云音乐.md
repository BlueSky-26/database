## ubuntu系统安装网易云音乐

1、去网易云音乐官网下载网易云音乐安装包

2、将下载好的安装包移动到某个文件下（个人选择）

3、打开终端，cd 回家，输入

```
sudo dpkg -i 安装包名字[属性复制粘贴过来]
```

​     命令执行结束会发现桌面上已经有了网易云音乐的icon



## 解决点击网易云音乐icon无法启动的问题

1、用root权限修改文件/usr/share/applications/netease-cloud-music.desktop

```
>>>sudo gedit /usr/share/applications/netease-cloud-music.desktop
修改执行参数:找到 Exec 那一行，在 = 后加上 sudo，%U 前面加上 --no-sandbox
即：Exec=sudo netease-cloud-music --no-sandbox %U
{说明：有些情况下不加 --no-sandbox 也是可以的}
```

2、cd 回家  修改/etc/sudoers文件，加一行内容；这样点击网易云音乐图标就是以管理员权限启动的了，且不用输入密码

```
>>>sudo gedit /etc/sudoers
在sudoers的内容下面加入下面的一行内容
YOURNAME ALL = NOPASSWD:/usr/bin/netease-cloud-music
YOURNAME换成登录的用户名
```

