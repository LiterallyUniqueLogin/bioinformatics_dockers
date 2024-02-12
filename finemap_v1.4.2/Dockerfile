FROM ubuntu:22.04

RUN apt-get update && apt-get upgrade -y
Run apt-get install wget libgomp1 -y

RUN mkdir -p /container_install/bin
ENV PATH="$PATH:/container_install/bin"
WORKDIR /container_install

RUN wget http://christianbenner.com/finemap_v1.4.2_x86_64.tgz
RUN tar xzvf finemap_v1.4.2_x86_64.tgz
RUN chmod +rx finemap_v1.4.2_x86_64
RUN chmod +rx finemap_v1.4.2_x86_64/finemap_v1.4.2_x86_64
RUN rm finemap_v1.4.2_x86_64.tgz
RUN ln -s ../finemap_v1.4.2_x86_64/finemap_v1.4.2_x86_64 bin/finemap
