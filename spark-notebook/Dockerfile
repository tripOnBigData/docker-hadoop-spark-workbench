FROM bde2020/hadoop-base:1.1.0-hadoop2.8-java8
MAINTAINER Ivan Ermilov <ivan.s.ermilov@gmail.com>

ENV APACHE_SPARK_VERSION 2.1.1
ENV APACHE_HADOOP_VERSION 2.8.0

RUN set -x \
    && curl -fSL "https://s3.eu-central-1.amazonaws.com/spark-notebook/tgz/spark-notebook-0.7.0-scala-2.11.8-spark-2.1.1-hadoop-2.8.0-with-hive.tgz?max-keys=100000" -o /tmp/spark-notebook.tgz \
    && tar -xzvf /tmp/spark-notebook.tgz -C /opt/ \
    && mv /opt/spark-notebook-* /opt/spark-notebook \
    && rm /tmp/spark-notebook.tgz

COPY run.sh /run.sh
RUN chmod a+x /run.sh

COPY application.conf /opt/spark-notebook/conf/
COPY clusters /opt/spark-notebook/conf/
COPY profiles /opt/spark-notebook/conf/

RUN mkdir -p /data/resources

ENV NOTEBOOKS_DIR /opt/spark-notebook/notebooks
ENV RESOURCES_DIR /data/resources
ENV SPARK_MASTER "spark://spark-master:7077"
ENV SPARK_EXECUTOR_MEMORY "2G"

WORKDIR /opt/spark-notebook/

CMD ["/run.sh"]
