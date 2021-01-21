FROM dominodatalab/base:Ubuntu18_DAD_Py3.7_R3.6_20200508

ENV HADOOP_VERSION=3.2.1
ENV HADOOP_HOME=/opt/hadoop
ENV HADOOP_CONF_DIR=/opt/hadoop/etc/hadoop
ENV SPARK_VERSION=3.0.0
ENV SPARK_HOME=/opt/spark

RUN wget -q https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-without-hadoop.tgz && \
        tar -xf spark-${SPARK_VERSION}-bin-without-hadoop.tgz && \
        rm spark-${SPARK_VERSION}-bin-without-hadoop.tgz && \
        mv spark-${SPARK_VERSION}-bin-without-hadoop $SPARK_HOME && \
        chmod -R 777 $SPARK_HOME/conf


RUN wget -q http://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
         tar -xf hadoop-${HADOOP_VERSION}.tar.gz && \
         rm hadoop-${HADOOP_VERSION}.tar.gz && \
         mv hadoop-${HADOOP_VERSION} $HADOOP_HOME
RUN echo 'export PATH="$PATH:$SPARK_HOME/bin:$HADOOP_HOME/bin"' >> $SPARK_HOME/conf/spark-env.sh        
RUN echo 'export SPARK_DIST_CLASSPATH="$(hadoop classpath):$HADOOP_HOME/share/hadoop/tools/lib/*"' >> $SPARK_HOME/conf/spark-env.sh

WORKDIR $SPARK_HOME/python
RUN python setup.py install
WORKDIR /

RUN wget -q http://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
         tar -xf hadoop-${HADOOP_VERSION}.tar.gz && \
         rm hadoop-${HADOOP_VERSION}.tar.gz && \
         mv hadoop-${HADOOP_VERSION} $HADOOP_HOME
RUN echo 'export PATH="$PATH:$SPARK_HOME/bin:$HADOOP_HOME/bin"' >> $SPARK_HOME/conf/spark-env.sh        
RUN echo 'export SPARK_DIST_CLASSPATH="$(hadoop classpath):$HADOOP_HOME/share/hadoop/tools/lib/*"' >> $SPARK_HOME/conf/spark-env.sh

RUN pip install spylon-kernel 
RUN python -m spylon_kernel install
