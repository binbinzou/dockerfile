FROM jenkins

USER root

#刷新包缓存 并且 安装wget工具
RUN apt-get update && apt-get install -y wget

#设置工作目录
WORKDIR /home

# 安装Maven
RUN wget http://apache-mirror.rbc.ru/pub/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz -O maven3.3.9.tar.gz
RUN tar xzvf maven3.3.9.tar.gz
RUN export PATH=maven3.3.9/bin:$PATH
RUN export PATH=/usr/local/bin/maven3.3.9/bin:$PATH
RUN ln -s /usr/local/bin/maven3.3.9/bin/mvn /usr/local/bin/mvn
RUN echo $PATH


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
RUN apt-get update && \
    apt-get -y install apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common && \
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
   add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable" && \
apt-get update && \
apt-get -y install docker-ce

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

RUN usermod -a -G staff jenkins

USER jenkins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

