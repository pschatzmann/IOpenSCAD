FROM ubuntu:groovy
LABEL maintainer="phil.schatzmann@gmail.com"
USER root
RUN apt-get update && apt-get install -y curl software-properties-common
RUN add-apt-repository ppa:openscad/releases
RUN curl -sL https://deb.nodesource.com/setup_15.x | bash -
RUN apt-get update && apt-get install -y git python3 python3-pip xvfb x11-utils nodejs
RUN apt update && apt install -y openscad
ENV PATH /opt/conda/envs/beakerx/bin:$PATH
RUN pip3 install --upgrade setuptools jupyterlab 
WORKDIR /opt
RUN git clone https://github.com/pschatzmann/openscad-kernel
WORKDIR /opt/openscad-kernel
RUN pip3 install .
RUN python3 -m iopenscad.install
RUN jupyter labextension install jupyterlab-openscad-syntax-highlighting
RUN jupyter labextension install jupyterlab-viewer-3d
RUN mkdir -p /home/openscad
WORKDIR /home/openscad
RUN cp /opt/openscad-kernel/documentation/* /home/openscad/
CMD jupyter lab --allow-root --ip=0.0.0.0 --port=8888 --no-browser 
