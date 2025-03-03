#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#
# -------------------------------------------------------------
# This Dockerfile creates a custom Docker image for Jupyter
# to use with the Apache Druid Jupyter notebook tutorials.
# Build using `docker build -t imply/druid-notebook:latest .`
# -------------------------------------------------------------

# Use the Jupyter base notebook as the base image
# Copyright (c) Project Jupyter Contributors.
# Distributed under the terms of the 3-Clause BSD License.
FROM jupyter/base-notebook

# Set the container working directory
WORKDIR /home/jovyan

# Install required Python packages
RUN pip install requests \
    pip install pandas \
    pip install numpy \
    pip install seaborn \
    pip install bokeh \
    pip install kafka-python \
    pip install sortedcontainers 

# Install druidapi client from apache/druid
# Local install requires sudo privileges 
USER root
ADD druidapi /home/jovyan/druidapi
WORKDIR /home/jovyan/druidapi
RUN pip install .



# WIP -- install DruidDataDriver as a package
# Import data generator and configuration file
# Change permissions to allow import (requires sudo privileges)

# The Jupyter notebooks themselves are mounted into the image's /home/jovyan/notebooks
# path when running this image.
RUN mkdir -p /home/jovyan/notebooks

WORKDIR /home/jovyan/notebooks
USER jovyan



# Add location of the data generator to PYTHONPATH
ENV PYTHONPATH "${PYTHONPATH}:/home/jovyan/notebooks/02-ingestion"

