#minos开源版本的安装使用
>https://github.com/zxl200406/minos

批量安装zookeeper,hdfs,hive,storm,kafka,hbase

---


###0、安装jdk
>使用jdk6，hadoop相关版本，运行在jdk6上

解压到/opt/soft目录
创建软件 jdk
vim /etc/profile

```
export JAVA_HOME=/opt/soft/jdk
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/rt.jar:$CLASSPATH
export LD_LIBRARY_PATH=$JAVA_HOME/jre/lib/amd64/server:$LD_LIBRARY_PATH
```
cd /usr/bin目录 创建软链

```
ln -s /opt/soft/jdk/bin/java java
ln -s /opt/soft/jdk/bin/javac javac
ln -s /opt/soft/jdk/bin/javadoc javadoc
ln -s /opt/soft/jdk/bin/javah javah
ln -s /opt/soft/jdk/bin/javap javap
```





###1、TANK的部署和上传

./build.sh start tank --tank\_ip 0.0.0.0 --tank\_port 80
官方我下载了一个hadoop 2.5.2版本 hadoop-2.5.2.tar.gz 
改名为hadoop-2.5.2-mdh2.2.1.tar.gz

图**一**
![tank](https://raw.githubusercontent.com/zxl200406/pic/master/pic/tank.png)

###2、部署supervisor
**修改minos/supervisor目录下的supervisord.conf文件**   
vim supervisord.conf
package_server=http://c3-pt-xxx.bj  必须是tank能访问web地址（图一地址）




###3、部署zookeeper
>安装一切hdfs storm...各类产品之前，必须先安装zookeeper

cd minos/config/conf/zookeeper   
cp zookeeper-dptst.cfg  zookeeper-c3ptstorm.cfg（c3ptstorm只是一个命名方式）   


vim zookeeper-c3ptstorm.cfg


```
  name=c3ptstorm(必须和zookeeper-c3ptstorm.cfg 后面字段相同)
  package_name=zookeeper-3.4.6-mdh1.1-SNAPSHOT.tar.gz（必须和tank  Package Name字段相同）
  revision=3.4.6-mdh1.1-SNAPSHOT （必须和tank  Revision No.字段相同）
  timestamp=20150921-164342 (必须和tank Timestamp 字段相同)
  
  host.0=10.108.X.220 # c3-pt-x01.bj
  host.1=10.108.X.221 # c3-pt-x02.bj
  host.2=10.108.X.222 # c3-pt-x03.bj
  host.3=10.108.X.223 # c3-pt-x04.bj
  host.4=10.108.X.224 # c3-pt-x05.bj
  
  这里的host.0，host.1  集群机器的IP地址
```

./deploy bootstrap zookeeper c3ptstorm
安装成功返回
![tank](https://raw.githubusercontent.com/zxl200406/pic/master/pic/873EE8AE-05AB-453A-8088-33A8C4460196.png)
