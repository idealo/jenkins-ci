FROM openshift/jenkins-slave-base-centos7

LABEL maintainer="dat.tran@idealo.de"

# Install miniconda
USER root
RUN yum install -y bzip2 gcc gcc-c++

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.3.31-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy

RUN chmod -R 777 /opt/conda

ENV PATH /opt/conda/bin:$PATH

# Install spark
ENV SPARK_HOME /opt/spark
ENV SPARK_URL http://d3kbcqa49mib13.cloudfront.net/spark-2.2.0-bin-hadoop2.7.tgz
ENV SPARK_FILENAME spark-2.2.0-bin-hadoop2.7.tgz
ENV PATH $PATH:$SPARK_HOME/bin

RUN mkdir $SPARK_HOME && \
    curl $SPARK_URL > $SPARK_HOME/$SPARK_FILENAME && \
    tar -xzf $SPARK_HOME/$SPARK_FILENAME --directory $SPARK_HOME --strip-components 1 && \
    rm $SPARK_HOME/$SPARK_FILENAME

USER 1001
