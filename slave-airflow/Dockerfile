FROM idealo/jenkins-slave-python-centos7

LABEL maintainer="christopher.lennan@idealo.de"

USER root

COPY environment.yml .

# Create conda environment and install dependencies
RUN conda env create -f environment.yml && source activate myapp

ENV AIRFLOW_HOME=/home/airflow
RUN mkdir -p ${AIRFLOW_HOME}
RUN chmod -R 775 ${AIRFLOW_HOME}

USER 1001
