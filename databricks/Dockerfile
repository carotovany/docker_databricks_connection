FROM ubuntu:20.04
RUN apt-get update && apt-get -y install sudo
RUN sudo apt-get -y install software-properties-common

### INSTALL PYTHON
RUN sudo apt-get -y install libssl-dev openssl
RUN sudo apt-get -y install libreadline-gplv2-dev libffi-dev
RUN sudo apt-get -y install libncursesw5-dev libsqlite3-dev
RUN sudo apt-get -y install tk-dev libgdbm-dev libc6-dev libbz2-dev 
RUN sudo apt-get -y install  wget
RUN apt-get update && apt-get install make
RUN sudo apt-get -y install zlib1g-dev
RUN apt-get -y install gcc mono-mcs && \
    rm -rf /var/lib/apt/lists/*
RUN wget https://www.python.org/ftp/python/3.7.10/Python-3.7.10.tgz
RUN tar xzvf Python-3.7.10.tgz
RUN ./Python-3.7.10/configure
RUN sudo make install
RUN alias python=python3


### INSTALL JAVA
RUN sudo add-apt-repository ppa:openjdk-r/ppa
RUN sudo apt-get install -y openjdk-8-jre

### INSTALL DATABRICKS-CONNECT
RUN pip3 install --upgrade pip
RUN pip3 uninstall pyspark
RUN pip3 install -U databricks-connect==7.3.*

RUN export DATABRICKS_HOST=${{ secrets.DATABRICKS_HOST }} && \
    export DATABRICKS_API_TOKEN=${{ secrets.DATABRICKS_API_TOKEN }} && \
    export DATABRICKS_ORG_ID=${{ secrets.DATABRICKS_ORG_ID }} && \
    export DATABRICKS_PORT=${{ secrets.DATABRICKS_PORT }} && \
    export DATABRICKS_CLUSTER_ID=${{ secrets.DATABRICKS_CLUSTER_ID }} && \
    echo "{\"host\": \"${DATABRICKS_HOST}\",\"token\": \"${DATABRICKS_API_TOKEN}\",\"cluster_id\":\"${DATABRICKS_CLUSTER_ID}\",\"org_id\": \"${DATABRICKS_ORG_ID}\", \"port\": \"${DATABRICKS_PORT}\" }" >> /root/.databricks-connectENV SPARK_HOME=/usr/local/lib/python3.7/site-packages/pyspark
