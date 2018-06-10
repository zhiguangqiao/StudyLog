## Rails服务Log文件无限增长问题
#### Apache 默认的 Log 处理
听说 Apache 默认配置，就可以实现将 log 文件定期整理成 access.log.1, access.log.2.gz, access.log.3.gz 等，不会存在日志文件无限膨胀的问题
#### Rails项目Log无限增长
Rails貌似没有Apache类似的日志处理能力，所以Rails服务的 log 文件以及相关sidekiq 的 log文件、 会越来越大，如果不去处理它，撑爆你的磁盘只是时间问题  
除此之外，处理一个单个的庞大日志文件也常常是件十分棘手的事
#### Logrotate定期整理Log
[[相关文档]](https://linux.die.net/man/8/logrotate)  
 logrotate是个十分有用的工具，它可以自动对日志进行截断（或轮循）、压缩以及删除旧的日志文件。例如，你可以设置logrotate，让/var/log/foo日志文件每30天轮循，并删除超过6个月的日志。配置完后，logrotate的运作完全自动化，不必进行任何进一步的人为干预。另外，旧日志也可以通过电子邮件发送，不过该选项超出了本教程的讨论范围
##### 安装
主流Linux发行版上都默认安装有logrotate包，如果出于某种原因，logrotate没有出现在里头，你可以使用apt-get或yum命令来安装。 
###### 安装命令 
Debian/Ubuntu `apt-get install logrotate cron`  
Fedora，CentOS或RHEL `yum install logrotate crontabs`

##### 配置使用
logrotate的配置文件是/etc/logrotate.conf，通常不需要对它进行修改。日志文件的轮循设置在独立的配置文件中，它（们）放在/etc/logrotate.d/目录下
###### 配置文件
创建文件 `vim /etc/logrotate.d/log-file `
添加配置内容   

```
/var/log/log-file {
    monthly
    rotate 5
    compress
    delaycompress
    missingok
    notifempty
    dateext
    create 644 root root
    postrotate
        /usr/bin/killall -HUP rsyslogd
    endscript
}

```

###### 配置字段解释
`monthly`  
: 日志文件将按月轮循。其它可用值为‘daily’，‘weekly’或者‘yearly’。  
`rotate 5`  
: 一次将存储5个归档日志。对于第六个归档，时间最久的归档将被删除。  
`compress`  
: 在轮循任务完成后，已轮循的归档将使用gzip进行压缩。  
`delaycompress`  
: 总是与compress选项一起用，delaycompress选项指示logrotate不要将最近的归档压缩，压缩将在下一次轮循周期进行。这在你或任何软件仍然需要读取最新归档时很有用。  
`missingok`  
: 在日志轮循期间，任何错误将被忽略，例如“文件无法找到”之类的错误。  
`notifempty`  
: 如果日志文件为空，轮循不会进行。  
`create 644 root root`  
: 以指定的权限创建全新的日志文件，同时logrotate也会重命名原始日志文件。  
`postrotate/endscript`  
: 在所有其它指令完成后，postrotate和endscript里面指定的命令将被执行。在这种情况下，rsyslogd 进程将立即再次读取其配置并继续运行。  
`dateext`  
:我们想要让旧日志文件以创建日期命名

另一个配置

```
/var/log/log-file {
    size=50M
    rotate 5
    dateext
    create 644 root root
    postrotate
        /usr/bin/killall -HUP rsyslogd
    endscript
}
```
