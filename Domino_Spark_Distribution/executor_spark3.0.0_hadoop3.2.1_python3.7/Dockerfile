FROM bitnami/spark:3.0.0

ENV HADOOP_VERSION=3.2.1
ENV SPARK_VERSION=3.0.0
ENV HADOOP_HOME=/opt/bitnami/hadoop
ENV HADOOP_CONF_DIR=/opt/bitnami/hadoop/etc/hadoop
ENV SPARK_HOME=/opt/bitnami/spark

USER root

RUN rm -rf /opt/bitnami/python
RUN apt-get update && apt-get install -y wget && rm -r /var/lib/apt/lists /var/cache/apt/archives
RUN ln -s /usr/bin/python3.7 /usr/bin/python

WORKDIR /opt/bitnami

RUN wget -q http://archive.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz && \
         tar -xf hadoop-$HADOOP_VERSION.tar.gz && \
         rm hadoop-$HADOOP_VERSION.tar.gz && \
         mv hadoop-$HADOOP_VERSION ${HADOOP_HOME}

RUN rm -rf ${SPARK_HOME}
RUN wget -q https://archive.apache.org/dist/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-without-hadoop.tgz && \
         tar -xf spark-$SPARK_VERSION-bin-without-hadoop.tgz && \
         rm spark-$SPARK_VERSION-bin-without-hadoop.tgz && \
         mv spark-$SPARK_VERSION-bin-without-hadoop ${SPARK_HOME} && \
         chmod -R 777 ${SPARK_HOME}/conf

RUN echo 'export SPARK_DIST_CLASSPATH="$(hadoop classpath):${HADOOP_HOME}/share/hadoop/tools/lib/*"' >> ${SPARK_HOME}/conf/spark-env.sh

WORKDIR /
RUN /opt/bitnami/scripts/spark/postunpack.sh
WORKDIR /opt/bitnami/spark
USER 1001
