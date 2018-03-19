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

USER 1001