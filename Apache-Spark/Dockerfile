# Dockerfile for installing Apache Spark v2.3.0 in a container
# For Java 
FROM openjdk:8

LABEL maintainer="aditisrinivas97@gmail.com"

# Download URL for spark version 2.3.0
ARG SPARK_DOWNLOAD_URL=http://www-eu.apache.org/dist/spark/spark-2.3.0/spark-2.3.0-bin-hadoop2.7.tgz

# Set the environment
ENV SPARK_HOME  /usr/local/spark

# Set user and working directory
USER root
WORKDIR /root

# Update apt-get and install vim screen tmux and spark
RUN apt-get -yqq update && \
    apt-get install -yqq vim screen tmux && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    wget -qO - ${SPARK_DOWNLOAD_URL} | tar -xz -C /usr/local/ && \
    # Add symbolic link for convinience 
    ln -s /usr/local/spark-2.3.0-bin-hadoop2.7 /usr/local/spark && \    
    # Copy the templates into the actual config files                                
    cp /usr/local/spark/conf/log4j.properties.template /usr/local/spark/conf/log4j.properties && \
    cp /usr/local/spark/conf/spark-defaults.conf.template /usr/local/spark/conf/spark-defaults.conf

# SparkContext web UI    : 4040 
# Spark master’s web UI  : 8080
# Spark worker web UI    : 8081
# Spark history web UI   : 18080
EXPOSE 4040 8080 8081 18080

# Start shell
CMD ["/bin/bash"]