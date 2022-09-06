ARG BASE_IMAGE=jupyter/base-notebook:ubuntu-22.04

FROM ${BASE_IMAGE}

USER root
# Ensure apt-get won't prompt for selecting options
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y \
    libsndfile1 sox libsox-fmt-all \
    libfreetype6 \
    python-setuptools swig \
    ffmpeg && \
    rm -rf /var/lib/apt/lists/*


USER jovyan
RUN python -m pip install pandas==1.4.4 sox==1.4.1 pandarallel==1.6.3 ipywidgets==8.0.2 omegaconf==2.2.3

RUN mkdir /home/jovyan/work/nb /home/jovyan/work/data /home/jovyan/work/logs
COPY assets/nb/*.ipynb /home/jovyan/work/nb/
COPY assets/data/*.* /home/jovyan/work/data/
USER root
RUN chown -R jovyan:users /home/jovyan/work/*
USER jovyan
