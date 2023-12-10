FROM nvcr.io/nvidia/cuda:12.1.0-devel-ubuntu22.04
WORKDIR /opt/mtr

ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0 7.5 8.0 8.6+PTX" \
    TORCH_NVCC_FLAGS="-Xfatbin -compress-all"

ENV DEBIAN_FRONTEND="noninteractive"
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-dev python3-pip python-is-python3 wget

COPY data data
COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt && pip install --no-cache-dir waymo-open-dataset-tf-2-11-0
RUN wget https://raw.githubusercontent.com/protocolbuffers/protobuf/main/python/google/protobuf/internal/builder.py -O /usr/local/lib/python3.10/dist-packages/google/protobuf/internal/builder.py

COPY mtr mtr
COPY setup.py setup.py
RUN python setup.py develop

COPY tools tools
