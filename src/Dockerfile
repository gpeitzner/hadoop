FROM ubuntu:latest
RUN apt update 
RUN apt upgrade -y
RUN apt autoremove -y
RUN DEBIAN_FRONTEND=noninteractive apt install openjdk-8-jdk -y
RUN apt install ssh -y
RUN apt install pdsh -y
RUN apt install nano -y
RUN wget https://downloads.apache.org/hadoop/common/hadoop-3.2.2/hadoop-3.2.2.tar.gz
RUN tar -xzf hadoop-3.2.2.tar.gz
ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
ENV HADOOP_HOME=/hadoop-3.2.2
RUN echo export HADOOP_HOME=/hadoop-3.2.2 >> ~/.bashrc
RUN echo export PATH=$HADOOP_HOME/bin:$PATH >> ~/.bashrc
RUN echo export HADOOP_CLASSPATH=$(/hadoop-3.2.2/bin/hadoop classpath) >> ~/.bashrc
WORKDIR /hadoop-3.2.2/WordCountExample
RUN mkdir WordCountExample
RUN wget https://ccl.cse.nd.edu/operations/hadoop/WordCount.java
RUN javac -classpath $($HADOOP_HOME/bin/hadoop classpath) WordCount.java 
RUN jar -cvf WordCount.jar *.class
COPY ./data.txt data.txt
RUN $HADOOP_HOME/bin/hadoop jar WordCount.jar WordCount ./data.txt ./outputs
RUN $HADOOP_HOME/bin/hadoop fs -cat ./outputs/part-r-00000
WORKDIR /hadoop-3.2.2/