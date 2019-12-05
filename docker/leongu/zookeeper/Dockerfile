FROM leongu2003/jdk8:latest

ENV ZOOKEEPER_VERSION "3.5.6"

RUN mkdir /opt/zookeeper &&\
	wget https://mirrors.tuna.tsinghua.edu.cn/apache/zookeeper/zookeeper-$ZOOKEEPER_VERSION/apache-zookeeper-$ZOOKEEPER_VERSION-bin.tar.gz -P /opt/zookeeper

RUN tar zxvf /opt/zookeeper/apache-zookeeper*.tar.gz -C /opt/zookeeper &&\
    chown -R root:root /opt/zookeeper/ &&\
    echo "4lw.commands.whitelist=*" >> /opt/zookeeper/apache-zookeeper-$ZOOKEEPER_VERSION-bin/conf/zoo_sample.cfg

ENV ZOOKEEPER_HOME /opt/zookeeper/apache-zookeeper-$ZOOKEEPER_VERSION-bin
ENV PATH $PATH:$ZOOKEEPER_HOME/bin

# RUN echo "source /root/.bash_profile" > /opt/zookeeper/start.sh &&\
# 	echo "cp /opt/zookeeper/apache-zookeeper-"$ZOOKEEPER_VERSION"-bin/conf/zoo_sample.cfg /opt/zookeeper/apache-zookeeper-"$ZOOKEEPER_VERSION"-bin/conf/zoo.cfg" >> /opt/zookeeper/start.sh &&\
# 	echo "/opt/zookeeper/apache-zookeeper-$"ZOOKEEPER_VERSION"-bin/bin/zkServer.sh start-foreground" >> /opt/zookeeper/start.sh

RUN echo "source /root/.bash_profile" > /opt/zookeeper/start.sh &&\
	echo "cp /opt/zookeeper/apache-zookeeper-"$ZOOKEEPER_VERSION"-bin/conf/zoo_sample.cfg /opt/zookeeper/apache-zookeeper-"$ZOOKEEPER_VERSION"-bin/conf/zoo.cfg" >> /opt/zookeeper/start.sh &&\
	echo "[ ! -z $""ZOOKEEPER_PORT"" ] && sed -i 's%.*clientPort=.*$%clientPort='$""ZOOKEEPER_PORT'""%g'  /opt/zookeeper/apache-zookeeper-"$ZOOKEEPER_VERSION"-bin/conf/zoo.cfg" >> /opt/zookeeper/start.sh &&\
	echo "[ ! -z $""ZOOKEEPER_ID"" ] && mkdir -p /tmp/zookeeper && echo $""ZOOKEEPER_ID > /tmp/zookeeper/myid" >> /opt/zookeeper/start.sh &&\
	echo "[[ ! -z $""ZOOKEEPER_SERVERS"" ]] && for server in $""ZOOKEEPER_SERVERS""; do echo $""server"" >> /opt/zookeeper/apache-zookeeper-"$ZOOKEEPER_VERSION"-bin/conf/zoo.cfg; done" >> /opt/zookeeper/start.sh &&\
	echo "/opt/zookeeper/apache-zookeeper-$"ZOOKEEPER_VERSION"-bin/bin/zkServer.sh start-foreground" >> /opt/zookeeper/start.sh

EXPOSE 2181

WORKDIR /opt/zookeeper/apache-zookeeper-$ZOOKEEPER_VERSION-bin

# CMD ["tail -f /opt/zookeeper/start.sh"]
ENTRYPOINT ["sh", "/opt/zookeeper/start.sh"]


