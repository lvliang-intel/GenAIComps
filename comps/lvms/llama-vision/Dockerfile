# Copyright (C) 2024 Intel Corporation
# SPDX-License-Identifier: Apache-2.0

# HABANA environment
# FROM vault.habana.ai/gaudi-docker/1.16.1/ubuntu22.04/habanalabs/pytorch-installer-2.2.2:latest as hpu
FROM opea/habanalabs:1.16.1-pytorch-installer-2.2.2 as hpu

ENV LANG=en_US.UTF-8

RUN apt-get update && apt-get install -y --no-install-recommends --fix-missing \
    git-lfs \
    libgl1-mesa-glx \
    libjemalloc-dev

RUN useradd -m -s /bin/bash user && \
    mkdir -p /home/user && \
    chown -R user /home/user/

USER user

RUN git lfs install

COPY comps /home/user/comps

#RUN pip install --no-cache-dir --upgrade-strategy eager transformers
RUN pip install transformers-4.45.0.dev0-py3-none-any.whl

RUN cd /home/user/comps/lvms/llama-vision/ && \
    pip install --no-cache-dir -r requirements.txt

ENV PYTHONPATH=/root:/home/user

WORKDIR /home/user/comps/lvms/llama-vision/

ENTRYPOINT ["python", "lvm.py"]
