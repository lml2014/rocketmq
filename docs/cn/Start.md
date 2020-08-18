# 运行RocketMQ
下载源码后，如何启动rocketmq，开始本地调试。

## Download & Build from Release
> unzip rocketmq-all-4.6.1-source-release.zip
> cd rocketmq-all-4.6.1/
> mvn -Prelease-all -DskipTests clean install -U
> cd distribution/target/apache-rocketmq

## Start Name Server

### sh脚本
path:distribution/target/rocketmq-4.6.1/rocketmq-4.6.1/bin
> nohup sh bin/mqnamesrv &
> tail -f ~/logs/rocketmqlogs/namesrv.log

The Name Server boot success...

### debug
Main class:org.apache.rocketmq.namesrv.NamesrvStartup
Working directory:/Users/shuishan/Project/project_git/rocketmq
Environment variables:ROCKETMQ_HOME=/Users/shuishan/Project/project_git/rocketmq

## Start Broker

### sh脚本
path:distribution/target/rocketmq-4.6.1/rocketmq-4.6.1/bin
> nohup sh bin/mqbroker -n localhost:9876 &
> tail -f ~/logs/rocketmqlogs/broker.log 

The broker[%s, 172.30.30.233:10911] boot success...

### debug
Main class:org.apache.rocketmq.broker.BrokerStartup
Program arguments:-c /Users/shuishan/Project/project_git/rocketmq/conf/broker.conf
Working directory:/Users/shuishan/Project/project_git/rocketmq
Environment variables:ROCKETMQ_HOME=/Users/shuishan/Project/project_git/rocketmq

## Send & Receive Messages

### sh脚本
> export NAMESRV_ADDR=localhost:9876
> sh bin/tools.sh org.apache.rocketmq.example.quickstart.Producer

SendResult [sendStatus=SEND_OK, msgId= ...

> sh bin/tools.sh org.apache.rocketmq.example.quickstart.Consumer
 
ConsumeMessageThread_%d Receive New Messages: [MessageExt...

## debug
启动Produce：org.apache.rocketmq.example.quickstart.Producer
启动Consume：org.apache.rocketmq.example.quickstart.Consumer

## Shutdown Servers

### sh脚本
> sh bin/mqshutdown broker

The mqbroker(36695) is running...
Send shutdown request to mqbroker(36695) OK

> sh bin/mqshutdown namesrv

The mqnamesrv(36664) is running...
Send shutdown request to mqnamesrv(36664) OK

## debug
关闭debug

## rocketmq-console
github:git@github.com:apache/rocketmq-externals.git
启动项目：rocketmq-externals/rocketmq-console

