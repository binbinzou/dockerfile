FROM jenkins

USER root

#刷新包缓存 并且 安装wget工具
RUN apt-get update && apt-get install -y wget
#设置工作目录
# WORKDIR /home
# 安装jdk
# ubuntu
# RUN wget http://download.oracle.com/otn/java/jdk/8u172-b11/a58eab1ec242421181065cdc37240b08/jdk-8u172-linux-x64.tar.gz?AuthParam=1532791575_5289ea2b5415845a4e407f41037dd314  -O jdk8.tar.gz
# RUN tar -zxvf jdk8.tar.gz
# 配置环境变量
# ENV JAVA_HOME /home/jdk1.7.0_79
# ENV JRE_HOME $JAVA_HOME/jre
# ENV CLASSPATH .:$JAVA_HOME/lib:$JRE_HOME/lib
# ENV PATH $PATH:$JAVA_HOME/bin
# 安装Doker
RUN apt-get update && apt-get install -y docker


RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

USER jenkins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

