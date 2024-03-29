from continuumio/miniconda3
SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get upgrade -y
# Utilities for managing the build
RUN apt-get install -y wget unzip
# Necessary for firefox (which will be installed via conda) which is necessary for bokeh export plots
RUN apt-get install -y libgtk-3-0 libasound2 libdbus-glib-1-2 libx11-xcb-dev libpci-dev libgl1-mesa-glx
# necessary for finemap, for some reason conda's install of libgomp doesn't satisfy the dependency
RUN apt-get install -y libgomp1

RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge
RUN conda config --set channel_priority true
RUN conda init --system bash

RUN conda install mamba -y
RUN mamba update --all -y

COPY env.yml .
RUN mamba env create --file=env.yml -n audit
RUN rm env.yml

RUN mkdir -p /container_install/bin
ENV PATH="$PATH:/container_install/bin"
COPY envsetup /container_install/bin/envsetup
RUN chmod a+rx /container_install/bin/envsetup

WORKDIR /container_install
RUN wget https://primus.gs.washington.edu/docroot/versions/PRIMUS_v1.9.0.tgz
# RUN mkdir PRIMUS_v1.9.0
RUN tar -xzvf PRIMUS_v1.9.0.tgz
RUN chmod -R a+rx PRIMUS_v1.9.0
RUN rm PRIMUS_v1.9.0.tgz
ENV PATH="$PATH:/container_install/PRIMUS_v1.9.0/bin"

# Could get a different instruction set for AMD processors
RUN wget https://s3.amazonaws.com/plink2-assets/alpha3/plink2_linux_avx2_20221024.zip
RUN unzip plink2_linux_avx2_20221024.zip -d bin
RUN rm plink2_linux_avx2_20221024.zip

# install a trtools branch
RUN envsetup conda remove --force trtools -y
RUN mkdir trtools
RUN git clone https://github.com/gymreklab/TRTools.git trtools --branch associaTR_plotting
WORKDIR trtools
RUN envsetup pip install -e .
WORKDIR ..

RUN wget http://christianbenner.com/finemap_v1.4.2_x86_64.tgz
RUN tar xzvf finemap_v1.4.2_x86_64.tgz
RUN chmod +rx finemap_v1.4.2_x86_64
RUN chmod +rx finemap_v1.4.2_x86_64/finemap_v1.4.2_x86_64
RUN rm finemap_v1.4.2_x86_64.tgz
RUN ln -s ../finemap_v1.4.2_x86_64/finemap_v1.4.2_x86_64 bin/finemap


