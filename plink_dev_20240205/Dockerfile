FROM ubuntu:22.04

RUN apt-get update && apt-get upgrade -y

RUN mkdir -p /container_install/bin
ENV PATH="$PATH:/container_install/bin"
WORKDIR /container_install

RUN apt-get install -y wget unzip
RUN wget https://s3.amazonaws.com/plink2-assets/plink2_linux_avx2_20240205.zip 
RUN unzip plink2_linux_avx2_20240205.zip -d bin
RUN rm plink2_linux_avx2_20240205.zip

