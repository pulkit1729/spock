FROM ubuntu:18.04
LABEL image=Spark-base-image
COPY --from=python:3.6 / /

ENV DAEMON_RUN=true
ENV SPARK_VERSION=3.0.1
ENV HADOOP_VERSION=2.7
ENV SCALA_VERSION=2.12.3
ENV SCALA_HOME=/usr/share/scala
ENV SPARK_HOME=/spark
ENV SPARK_OPTS --driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M --driver-java-options=-Dlog4j.logLevel=info
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.7-src.zip
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64/
ENV PYSPARK_PYTHON python3

CMD mkdir /user/spark

RUN  apt-get update \
  && apt-get install -y wget \
  && apt-get install -y coreutils \
  && apt-get install -y procps \
  && apt-get install -y openssl \
  && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
  apt-get install -y openjdk-11-jdk && \
  apt-get install -y ant && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/ && \
  rm -rf /var/cache/oracle-jdk8-installer;

RUN export JAVA_HOME

RUN cd "/tmp" && \
  wget "https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
  tar xzf "scala-${SCALA_VERSION}.tgz" && \
  mkdir "${SCALA_HOME}" && \
  rm "/tmp/scala-${SCALA_VERSION}/bin/"*.bat && \
  mv "/tmp/scala-${SCALA_VERSION}/bin" "/tmp/scala-${SCALA_VERSION}/lib" "${SCALA_HOME}" && \
  ln -s "${SCALA_HOME}/bin/"* "/usr/bin/" && \
  rm -rf "/tmp/"*

RUN export PATH="/usr/local/sbt/bin:$PATH" && mkdir -p "/usr/local/sbt"

RUN wget http://mirror.ox.ac.uk/sites/rsync.apache.org/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

# Install Spark and move it to the folder "/spark" and then add this location to the PATH env variable
RUN tar -xzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
  mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} /spark && \
  rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
  export PATH=$SPARK_HOME/bin:$PATH




