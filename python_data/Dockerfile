from mambaorg/micromamba:latest
SHELL ["/bin/bash", "-c"]

USER root
RUN apt-get update && apt-get upgrade -y

# Necessary for firefox (which will be installed via conda) which is necessary for bokeh export plots
RUN apt-get install -y libgtk-3-0 libasound2 libdbus-glib-1-2 libx11-xcb-dev libpci-dev libgl1-mesa-glx
# necessary for finemap, for some reason conda's install of libgomp doesn't satisfy the dependency
RUN apt-get install -y libgomp1

USER 1001
COPY --chown=$MAMBA_USER:$MAMBA_USER env.yml /tmp/env.yml
RUN micromamba install -y -n base -f /tmp/env.yml && \
    micromamba clean --all --yes

# Our goal is to get bash executed in this docker container via Cromwell
# container to have an already activated conda environment
# the default cromwell.conf file executes docker with --entrypoint /bin/bash
# firstly, this ignores the default entrypoint in the micromomba docker 
# that this docker is built off of which would have activated the base environment.
# Further, the bash shell invocated that way is neither login nor interactive,
# and so will ignore any bashrc or profile files that would normally contain
# the conda initialization code.
# To work around that, use a environment variable to tell bash
# to execute a file regardless of how it starts up
# and have that file contain the important parts of mamba initialization
# (gotten from reading the output that micromamba shell init -s bash
# spits into the .bashrc file)
# as well as a command to activate the base environment.
USER root
RUN mkdir /container_install
COPY activate_env /container_install/activate_env
USER 1001
ENV BASH_ENV=/container_install/activate_env

