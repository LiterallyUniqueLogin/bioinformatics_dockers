from continuumio/miniconda3
SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get upgrade -y
RUN git clone https://github.com/HipSTR-Tool/HipSTR
WORKDIR HipSTR
RUN make version && make
ENV PATH="$PATH:/HipSTR"
