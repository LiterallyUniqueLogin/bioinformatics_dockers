from mambaorg/micromamba:latest
SHELL ["/bin/bash", "-c"]

# USER root
RUN apt-get update && apt-get upgrade -y

COPY --chown=$MAMBA_USER:$MAMBA_USER env.yaml /tmp/env.yaml
RUN micromamba install -y -n base -f /tmp/env.yaml && \
    micromamba clean --all --yes

#RUN micromamba shell init -s bash

RUN mkdir -p /container_install/bin
ENV PATH="$PATH:/container_install/bin"
COPY envsetup /container_install/bin/envsetup
RUN chmod a+rx /container_install/bin/envsetup
#USER 1001

