## ubuntu下彻底删除mysql命令

### 删除 mysql

```
sudo apt-get autoremove --purge mysql-server
sudo apt-get remove mysql-server
sudo apt-get autoremove mysql-server
sudo apt-get remove mysql-common //这个很重要
```


上面的其实有一些是多余的

### 清理残留数据

```
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```