FROM centos:7.7.1908

RUN yum -y install zsh nc vim lsof wget tar bzip2 unzip vim-enhanced passwd sudo yum-utils hostname net-tools rsync man git make automake cmake patch logrotate python-devel libpng-devel libjpeg-devel pwgen python-pip

RUN mkdir /opt/java &&\
	wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u141-b15/336fa29ff2bb4ef291e347e091f7f4a7/jdk-8u141-linux-x64.tar.gz" -P /opt/java

RUN tar zxvf /opt/java/jdk-8u141-linux-x64.tar.gz -C /opt/java &&\
    chown -R root:root /opt/java
# or jdk1.8.0_141's owner will be 10:143

# jdk env
ENV JAVA_HOME /opt/java/jdk1.8.0_141
ENV JRE_HOME $JAVA_HOME/jre
ENV PATH $PATH:$JAVA_HOME/bin

# timezone
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' >/etc/timezone

#RUN tar zxvf /opt/java/jdk-8u141-linux-x64.tar.gz -C /opt/java &&\
#	JAVA_HOME=/opt/java/jdk1.8.0_141 &&\
#	sed -i "/^PATH/i export JAVA_HOME=$JAVA_HOME" /root/.bash_profile &&\
#	sed -i "s%^PATH.*$%&:$JAVA_HOME/bin%g" /root/.bash_profile &&\
#	source /root/.bash_profile


