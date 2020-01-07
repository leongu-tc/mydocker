FROM leongu2003/jdk8

ENV KAFKA_VERSION "2.3.1"

RUN mkdir /opt/kafka &&\
	wget http://mirror.bit.edu.cn/apache/kafka/$KAFKA_VERSION/kafka_2.11-$KAFKA_VERSION.tgz -P /opt/kafka

RUN tar zxvf /opt/kafka/kafka*.tgz -C /opt/kafka &&\
    chown -R root:root /opt/kafka/ &&\
	sed -i 's/num.partitions.*$/num.partitions=3/g' /opt/kafka/kafka_2.11-$KAFKA_VERSION/config/server.properties &&\
	echo -e "\ndelete.topic.enable=true" >> /opt/kafka/kafka_2.11-$KAFKA_VERSION/config/server.properties &&\
	echo -e "#port=9092" >> /opt/kafka/kafka_2.11-$KAFKA_VERSION/config/server.properties &&\
	echo -e "#advertised.host.name=yourhost" >> /opt/kafka/kafka_2.11-$KAFKA_VERSION/config/server.properties &&\
	echo -e "#host.name=yourhost" >> /opt/kafka/kafka_2.11-$KAFKA_VERSION/config/server.properties

ENV KAFKA_HOME /opt/kafka/kafka_2.11-$KAFKA_VERSION
ENV PATH $PATH:$KAFKA_HOME/bin

RUN echo "source /root/.bash_profile" > /opt/kafka/start.sh &&\
	echo "cd /opt/kafka/kafka_2.11-"$KAFKA_VERSION >> /opt/kafka/start.sh &&\
	echo "[ ! -z $""ZOOKEEPER_CONNECT"" ] && sed -i 's%.*zookeeper.connect=.*$%zookeeper.connect='$""ZOOKEEPER_CONNECT'""%g'  /opt/kafka/kafka_2.11-"$KAFKA_VERSION"/config/server.properties" >> /opt/kafka/start.sh &&\
	echo "[ ! -z $""BROKER_ID"" ] && sed -i 's%broker.id=.*$%broker.id='$""BROKER_ID'""%g'  /opt/kafka/kafka_2.11-"$KAFKA_VERSION"/config/server.properties" >> /opt/kafka/start.sh &&\
	echo "[ ! -z $""BROKER_PORT"" ] && sed -i 's%#port=.*$%port='$""BROKER_PORT'""%g'  /opt/kafka/kafka_2.11-"$KAFKA_VERSION"/config/server.properties" >> /opt/kafka/start.sh &&\
	echo "sed -i 's%#advertised.host.name=.*$%advertised.host.name='$""(hostname -i)'""%g'  /opt/kafka/kafka_2.11-"$KAFKA_VERSION"/config/server.properties" >> /opt/kafka/start.sh &&\
	echo "[ ! -z $""ADVERTISED_HOST_NAME"" ] && sed -i 's%advertised.host.name=.*$%advertised.host.name='$""ADVERTISED_HOST_NAME'""%g'  /opt/kafka/kafka_2.11-"$KAFKA_VERSION"/config/server.properties" >> /opt/kafka/start.sh &&\
	echo "sed -i 's%#host.name=.*$%host.name='$""(hostname -i)'""%g'  /opt/kafka/kafka_2.11-"$KAFKA_VERSION"/config/server.properties" >> /opt/kafka/start.sh &&\
	echo "[ ! -z $""HOST_NAME"" ] && sed -i 's%host.name=.*$%host.name='$""HOST_NAME'""%g'  /opt/kafka/kafka_2.11-"$KAFKA_VERSION"/config/server.properties" >> /opt/kafka/start.sh &&\
	echo "bin/kafka-server-start.sh config/server.properties" >> /opt/kafka/start.sh &&\
	chmod a+x /opt/kafka/start.sh

EXPOSE 9092

WORKDIR /opt/kafka/kafka_2.11-$KAFKA_VERSION

# CMD ["tail -f /opt/kafka/start.sh"]
ENTRYPOINT ["sh", "/opt/kafka/start.sh"]
