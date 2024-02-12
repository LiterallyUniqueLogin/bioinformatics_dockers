FROM ubuntu:22.04

RUN apt-get update && apt-get upgrade -y
Run apt-get install wget libgomp1 -y

RUN mkdir -p /container_install/bin
ENV PATH="$PATH:/container_install/bin"
WORKDIR /container_install

RUN wget http://christianbenner.com/ldstore_v2.0_x86_64.tgz
RUN tar xzvf ldstore_v2.0_x86_64.tgz
RUN chmod +rx ldstore_v2.0_x86_64
RUN chmod +rx ldstore_v2.0_x86_64/ldstore_v2.0_x86_64
RUN rm ldstore_v2.0_x86_64.tgz
RUN ln -s ../ldstore_v2.0_x86_64/ldstore_v2.0_x86_64 bin/ldstore
