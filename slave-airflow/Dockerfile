FROM openshift/jenkins-slave-base-centos7

LABEL maintainer="christopher.lennan@idealo.de"

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

# Create conda environment and install airflow, nose, pandas, psycopg2, s3fs, and scikit-learn
RUN conda create -n myapp \
    && source activate myapp \
    && conda install -y -c conda-forge \
      airflow=1.9.* \
      nose=1.3.* \
      psycopg2=2.7.* \
      pandas=0.23.* \
      s3fs=0.1.* \
      scikit-learn=0.20*

ENV AIRFLOW_HOME=/home/airflow
RUN mkdir -p ${AIRFLOW_HOME}
RUN chmod -R 775 ${AIRFLOW_HOME}

USER 1001
