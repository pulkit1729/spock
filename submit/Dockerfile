FROM spark-base

ENV MASTER_CONTAINER_NAME=spark-master
ENV SPARK_EXECUTOR_MEMORY=6G
ENV SPARK_EXECUTOR_CORES=3

COPY requirements.txt .
RUN pip install -r requirements.txt


EXPOSE 4040 8888

WORKDIR /home/

ENTRYPOINT $SPARK_HOME/bin/spark-shell --conf spark.executor.memory=2G --conf spark.executor.cores=1 --master spark://spark-master:7077