FROM spark-base

ENV SPARK_VERSION=3.0.1
ENV JUPYTERLAB_VERSION=2.2.9

RUN apt-get update -y && \
    apt-get install -y python3-pip && \
    pip3 install pyspark${spark_version} jupyterlab${jupyterlab_version}

EXPOSE 8888

CMD jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --allow-root --NotebookApp.token=