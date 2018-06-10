#CentOS7安装Docker实战
## 
官方文档链接：https://docs.docker.com/install/linux/docker-ce/centos/  
安装顺利完成  
启动Docker服务失败  
启动命令失败  
`sudo systemctl start docker.service`

提示信息：  
`Job for docker.service failed because the control process exited with error code. See "systemctl status docker.service" and "journalctl -xe" for details.`

根据提示执行如下命令查看日志  
`journalctl -xe` 
 
日志信息

```

Apr 3 15:31:11 Docker dockerd: time="2018-04-03T15:31:11.835565555+08:00" level=info msg="devmapper: Creating filesystem xfs on device docker-253:1-34265854-base, mkfs args: [-m crc=0,finobt=0 /dev/mapper/docker-253:1-34265854-base]"
Apr 3 15:31:11 Docker dockerd: time="2018-04-03T15:31:11.836336636+08:00" level=info msg="devmapper: Error while creating filesystem xfs on device docker-253:1-34265854-base: exit status 1"
Apr 3 15:31:11 Docker dockerd: time="2018-04-03T15:31:11.836350296+08:00" level=error msg="[graphdriver] prior storage driver devicemapper failed: exit status 1"

```

问题原因是 mkfs.xfs 版本太低   
更新版本  
`yum update xfsprogs`

再次启动成功

解决问题参考资料：  
http://www.cnblogs.com/FoChen/p/8708932.html