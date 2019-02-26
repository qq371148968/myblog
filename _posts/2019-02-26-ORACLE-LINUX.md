---
title: oracle主机修改了ip怎么办？
date: 2019-02-26
categories: Linux
tags:oracle linux 网卡
- linux
- shell
---

*来源： 网络整合*

内容：
虚拟机迁移，ip地址变动，oracle服务不能用了怎么办？


1.为主机起名字,xxx.com
	修改hosts 文件

2.oracle监听文件不再配置ip地址，而是用上面的主机名字
	需改文件：listener.ora tnsnames.ora

```shell
[oracle@localhost ~]$ cd /u01/oracle/11g/network/admin/
[oracle@localhost ~]$ pwd
/u01/oracle/11g/network/admin
[oracle@localhost admin]$ ls
listener1709067AM0045.bak  shrept.lst               tnsnames1709067AM0045.bak
listener.ora               sqlnet1709067AM0045.bak  tnsnames.ora
samples                    sqlnet.ora
```

 修改后的：
LISTENER1 =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = xxx.com)(PORT = 1522))
    )
  )

3.重启网卡

Linux 下网卡重启的命令为：

 /etc/init.d/network restart 或者是  /etc/init.d/networking restart
或者重启网络服务：
service network restart