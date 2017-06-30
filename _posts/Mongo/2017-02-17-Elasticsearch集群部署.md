---
layout: life
title: Elasticsearch集群部署
category: Mongo
duoshuo: true
date: 2017-05-20
---

******

	作者: minus
	版本: V 0.0.1
	日期: 2017年05月20日
	mail: minus@stu.xjtu.edu.cn

<!-- more -->

*******

### Elasticseach集群架构
1. ES基本情况
```
ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。Elasticsearch是用Java开发的，并作为Apache许可条款下的开放源码发布，是当前流行的企业级搜索引擎。设计用于云计算中，能够达到实时搜索，稳定，可靠，快速，安装使用方便
```
2. 及集群服务器情况
```
整个集群的部署采用4台服务器，其中一台作为master，其他三台作为slaves
```

3. 各服务器配置参数(舆情集群实例)
```sh
======================================== master[yuqing4] - configuration =============================================================
---- Cluster ------
cluster.name: yuqing
---- Node ---------
node.name: node-yuqing4
---- Paths --------
path.data: /yuqing/elasticsearch/data
---- Network ------
network.bind_host: ['ip内网xx.xx.xx.xx', 'ip外网:xx.xx.xx.xx']
network.publish_host: ip内网xx.xx.xx.xx
---- Discovery -----
discovery.zen.ping.unicast.hosts: ['yuqing1-ip内网xx.xx.xx.xx', 'yuqing2-ip内网xx.xx.xx.xx', 'yuqing3-ip内网xx.xx.xx.xx', 'yuqing4-ip内网xx.xx.xx.xx']
---- Various -------
node.master: true
node.data: false
http.enabled: true
http.cors.enabled: true
http.cors.allow-origin: "*"
======================================== slave1 [yuqing1] - configuration =============================================================
---- Cluster -------
cluster.name: yuqing
----- Node ---------
node.name: node-yuqing1
----- Paths --------
path.data: /yuqing/elasticsearch/data
----- Network ------
network.bind_host: ['ip内网xx.xx.xx.xx']
network.publish_host: ip内网xx.xx.xx.xx
----- Discovery ----
discovery.zen.ping.unicast.hosts: ['yuqing1-ip内网xx.xx.xx.xx', 'yuqing2-ip内网xx.xx.xx.xx', 'yuqing3-ip内网xx.xx.xx.xx', 'yuqing4-ip内网xx.xx.xx.xx']
----- Various ------
node.master: false
node.data: true
http.enabled: true
http.cors.enabled: true
http.cors.allow-origin: "*"
======================================== slave2 [yuqing2] - configuration =============================================================
---- Cluster -------
cluster.name: yuqing
---- Node ----------
node.name: node-yuqing2
---- Paths ---------
path.data: /yuqing/elasticsearch/data
---- Network -------
network.bind_host: ['ip内网xx.xx.xx.xx']
network.publish_host: ip内网xx.xx.xx.xx
----- Discovery ----
discovery.zen.ping.unicast.hosts: ['yuqing1-ip内网xx.xx.xx.xx', 'yuqing2-ip内网xx.xx.xx.xx', 'yuqing3-ip内网xx.xx.xx.xx', 'yuqing4-ip内网xx.xx.xx.xx']
----- Various ------
node.master: false
node.data: true
http.enabled: true
http.cors.enabled: true
http.cors.allow-origin: "*"
======================================== slave3 [yuqing3] - configuration =============================================================
---- Cluster -------
cluster.name: yuqing
---- Node ----------
node.name: node-yuqing3
---- Paths ---------
path.data: /yuqing/elasticsearch/data
---- Network -------
network.bind_host: ['ip内网xx.xx.xx.xx']
network.publish_host: ip内网xx.xx.xx.xx
----- Discovery ----
discovery.zen.ping.unicast.hosts: ['yuqing1-ip内网xx.xx.xx.xx', 'yuqing2-ip内网xx.xx.xx.xx', 'yuqing3-ip内网xx.xx.xx.xx', 'yuqing4-ip内网xx.xx.xx.xx']
----- Various ------
node.master: false
node.data: true
http.enabled: true
http.cors.enabled: true
http.cors.allow-origin: "*"
```

### 安装[ES-Head for ES5.x](http://orchome.com/489)[https://github.com/mobz/elasticsearch-head]
```
1. 执行 'npm run start' 出现 '/usr/bin/env: node: No such file or directory' -
   解决方案：　'sudo apt-get install nodejs-legacy'
2. 安装步骤
    ```
    1. 下载npm
    sudo apt-get install nodejs
    sudo apt-get install nodejs-legacy   // 不安装这个不能执行npm
    ```
    2. 下载github代码
    ```
    git clone git://github.com/mobz/elasticsearch-head.git
    ```
    3. 进入 elasticsearch-head 目录
    ```
    cd elasticsearch-head
    ```
    4. npm安装包
    ```
    npm install
    ```
    5. 修改elasticsearch-head下Gruntfile.js文件
        connect: {
              server: {
                  options: {
                      host: '0.0.0.0',
                      port: 30005,  // 这个端口 为没有被占用的端口，用于访问head－web
                      base: '.',
                      keepalive: true
                  }
              }
          }
     6. 启动 es-head
     ```sh
     npm run start
     ```
     7. 查看浏览器配置
     ```
     http://xx.xx.xx.xx:30005
     在这个页面填写 elasticsearch的对外端口(默认9200)- 
     ```
```

### Ubuntu系统中设置开机启动服务
1. 将你的启动脚本复制到 /etc/init.d目录下
```
脚本文件为es - [内容如5]
```

2. 设置脚本文件权限
```
sudo chmod 755 /etc/init.d/es
```

3. 执行如下命令将脚本放到启动脚本中去
```
cd /etc/init.d
sudo -sH
# update-rc.d es defaults 95
备注: 其中数字95是脚本启动顺序号，按照自己的需要相应修改即可，在你有多个启动脚本，而它们之间又有先后启动的依赖关系时你就知道这个数字的具体作用了
执行之后应该出现如下信息:
update-rc.d: warning: /etc/init.d/test missing LSB information
update-rc.d: see <http://wiki.debian.org/LSBInitScripts>
  Adding system startup for /etc/init.d/test ...
    /etc/rc0.d/K95test -> ../init.d/test
    /etc/rc1.d/K95test -> ../init.d/test
    /etc/rc6.d/K95test -> ../init.d/test
    /etc/rc2.d/S95test -> ../init.d/test
    /etc/rc3.d/S95test -> ../init.d/test
    /etc/rc4.d/S95test -> ../init.d/test
    /etc/rc5.d/S95test -> ../init.d/test
```

4. 卸载启动脚本的方法
```
cd /etc/init.d
sudo -sH
# update-rc.d -f es remove
执行之后应该显示的信息:
Removing any system startup links for /etc/init.d/test ...
    /etc/rc0.d/K95test
    /etc/rc1.d/K95test
    /etc/rc2.d/S95test
    /etc/rc3.d/S95test
    /etc/rc4.d/S95test
    /etc/rc5.d/S95test
    /etc/rc6.d/K95test
```

5. es文件内容[es不能由root执行,里面的两个start()函数根据具体情况选择]

```
#!/bin/bash                                                                                                                                       
# chkconfig: 2345 10 90  
# description: Elasticsearch Service ....  
### BEGIN INIT INFO
# Provides:          scriptname
# Required-Start:    $remote_fs $syslog
# Required-Stop:     $remote_fs $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Start daemon at boot time
# Description:       Enable service provided by daemon.
### END INIT INFO
export JAVA_HOME=/var/www/tomcat/jdk1.8              # 需修改
export JRE_HOME=${JAVA_HOME}/jre                     # 需修改
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  # 需修改
export PATH=${JAVA_HOME}/bin:$PATH                   # 需修改
```
```
export ELA_HOME=/usr/local/elasticsearch-5.0.0/bin   # 需修改
export PATH=$ELA_HOME:$PATH                          # 需修改
```
```
ES_HOME=/usr/local/elasticsearch-5.0.0               # 需修改
EXEC_PATH=$ES_HOME                                   # 需修改
EXEC=elasticsearch                           
DAEMON=$EXEC_PATH/bin/$EXEC  
PID_FILE=$ES_HOME/pid/es.pid                         # 注意需要创建这个pid目录(es本身没有该目录)
ServiceName='Elasticsearch 5.0'                      # 可修改
```
```
# . /etc/rc.d/init.d/functions  
```
```
if [ ! -x $DAEMON ] ; then  
       echo "ERROR: $DAEMON not found"  
       exit 1   
fi  
```
```
stop()  
{  
       echo "Stoping $ServiceName ..."  
       ps aux | grep "$ES_HOME" | kill -9 `awk '{print $2}'`  >/dev/null 2>&1  
       rm -f $PID_FILE  
       sleep 1  
       echo "Shutting down $ServiceName: [  successful  ]"  
}  
```
```
start()   # 只能用于 ubuntu用户执行 service es start，不能使用root用户执行
{  
       echo "Starting $ServiceName ..."  
       $DAEMON >/dev/null 2>&1 &
       pidof $EXEC > $PID_FILE  
       sleep 1  
       echo "Starting $ServiceName: [  successful  ]"  
}  
```
```
start()   # 这个可以根据登陆用户选择执行方式,root用户执行时原理也是进入到非root的ubuntu下面执行
{  
       echo "Starting $ServiceName ..."  
       ulimit -n 65536
       if [`whoami` == "ubuntu"]
           then $DAEMON >/dev/null 2>&1 &
       else
           su ubuntu -c '/bin/sh /usr/local/elasticsearch-5.0.0/bin/elasticsearch >/dev/null 2>&1 &'
       fi  
       pidof $EXEC > $PID_FILE  
       sleep 1   
       echo "Starting $ServiceName: [  successful  ]"  
}  

```
```
restart()  
{  
    stop  
    start  
}  
```
```
case "$1" in  
    start)  
        start  
        ;;  
    stop)  
        stop  
        ;;  
    restart)  
        restart  
        ;;  
    status)  
        status -p $PID_FILE $DAEMON  
        ;;  
    *)  
        echo "Usage: service $ServiceName {start|stop|restart|status}"  
        exit 1  
esac  
exit $?              
```

6. cassandra开机启动文件
```
#!/bin/bash
# chkconfig: 2345 10 90
# description: CASSANDRA        
### BEGIN INIT INFO
# Provides:             name
# Required-Start:       $remote_fs $syslog
# Required-Stop:        $remote_fs $syslog
# Default-Start:        2 3 4 5
# Default-Stop:         0 1 6
# Short-Description:    Start daemon at boot time
# Description:          Enable service provided by daemon
# END INIT INFO
export JAVA_HOME=/usr/local/jdk1.8.0_121
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export CASSANDRA_PATH=/usr/local/apache-cassandra-3.10/bin
export PATH=$CASSANDRA_PATH:$PATH
start()
{
    echo "starting the cassandra..."
    su ubuntu -c "/usr/local/apache-cassandra-3.10/bin/cassandra > /home/ubuntu/cass.log"
    sleep 15
    echo "starting the kong..."
    su ubuntu -c "/usr/local/bin/kong start"
    echo "started the cassandra!!!"
}
stop()
{
    echo "stoping the kong..."
    su ubuntu -c "/usr/local/bin/kong stop"
    sleep 5
    echo "stoping the cassandra..."
    su ubuntu -c "pgrep -u ubuntu -f cassandra |  xargs kill -9"
    sleep 1
    echo "shutdown the cassandra!!!"
}
restart()
{
    stop
    start
}
case "$1" in
    start)
        start
        ;;
    stop)
        stop
        ;;
    restart)
        restart
        ;;
    *)
        echo "Usage: start|stop|restart"
        exit 1
esac
exit $?
```
