# Copyright (c) 2022-2025, NVIDIA CORPORATION & AFFILIATES. All rights reserved.
#
# See LICENSE for license information.

ARG MANYLINUX_BASE_IMAGE
FROM ${MANYLINUX_BASE_IMAGE}

ARG TORCH_VERSION=2.9.1
ARG CUDA_VERSION="${CUDA_MAJOR}.${CUDA_MINOR}"
ARG CUDNN_MAJOR_VERSION=9

# Install PyTorch
RUN export MATRIX_CUDA_VERSION=$(echo $CUDA_VERSION | awk -F \. {'print $1 $2'}) && \
    export MATRIX_TORCH_VERSION=$(echo $TORCH_VERSION | awk -F \. {'print $1 "." $2'}) && \
    export TORCH_CUDA_VERSION=$(/opt/python/cp${PYTHON_VERSION}-cp${PYTHON_VERSION}/bin/python -c "from os import environ as env; \ 
    minv = {'2.5': 118, '2.6': 118, '2.7': 118, '2.8': 126, '2.9': 126}[env['MATRIX_TORCH_VERSION']]; \
    maxv = {'2.5': 124, '2.6': 126, '2.7': 128, '2.8': 129, '2.9': 130}[env['MATRIX_TORCH_VERSION']]; \
    print(minv if int(env['MATRIX_CUDA_VERSION']) < 120 else maxv)" \
    ) && \
    /opt/python/cp${PYTHON_VERSION}-cp${PYTHON_VERSION}/bin/pip install --no-cache-dir torch==${TORCH_VERSION} --index-url https://download.pytorch.org/whl/cu${TORCH_CUDA_VERSION}

