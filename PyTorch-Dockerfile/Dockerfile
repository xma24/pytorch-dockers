
FROM nvidia/cuda:11.3.1-devel-ubuntu20.04


# The following code is to solve GPG key problem; https://forums.developer.nvidia.com/t/notice-cuda-linux-repository-key-rotation/212771/5
RUN sh -c 'echo "APT { Get { AllowUnauthenticated \"1\"; }; };" > /etc/apt/apt.conf.d/99allow_unauth'

RUN apt -o Acquire::AllowInsecureRepositories=true -o Acquire::AllowDowngradeToInsecureRepositories=true update
RUN apt-get install -y curl wget

RUN apt-key del 7fa2af80
RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb
RUN dpkg -i cuda-keyring_1.0-1_all.deb
RUN rm -f /etc/apt/sources.list.d/cuda.list /etc/apt/apt.conf.d/99allow_unauth cuda-keyring_1.0-1_all.deb
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A4B469963BF863CC F60F4B3D7FA2AF80
RUN apt-get update && apt-get upgrade -y
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    curl \
    ca-certificates \
    sudo \
    git \
    bzip2 \
    libx11-6 \
    python3-dev \
    wget \ 
    libxext6 \
    ffmpeg \
    libsm6 \
    graphviz \
    gcc \
    g++ \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /home
RUN adduser --disabled-password --gecos '' --shell /bin/bash user && chown -R user:user /home
RUN echo "user ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-user
USER user
ENV HOME=/home/user

# Install Miniconda and Python 3.8
ENV CONDA_AUTO_UPDATE_CONDA=false
ENV PATH=/usr/local/lib/:$PATH
ENV PATH=/home/user/.local/lib/:$PATH
ENV PATH=/home/user/.local/bin/:$PATH
ENV PATH=/home/user/.local/lib/python3.8/site-packages/:$PATH

ENV PATH=/home/user/miniconda/bin:$PATH
RUN curl -sLo ~/miniconda.sh https://repo.continuum.io/miniconda/Miniconda3-py38_4.8.3-Linux-x86_64.sh \
    && chmod +x ~/miniconda.sh \
    && ~/miniconda.sh -b -p ~/miniconda \
    && rm ~/miniconda.sh \
    && conda install -y python==3.8.3 \
    && conda clean -ya

RUN pip install torch==1.11.0+cu113 torchvision==0.12.0+cu113 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113 \
    && pip --no-cache-dir install nvidia-pyindex==1.0.9 \
    && pip --no-cache-dir install pytorch-quantization==2.1.2 \
    # && pip install torch-tensorrt -f https://github.com/NVIDIA/Torch-TensorRT/releases \
    # >>> Install PyTorch Lightning
    && pip install pytorch_lightning==1.6.4 \
    && pip --no-cache-dir install rich==12.4.4 \
    && pip --no-cache-dir install termcolor==1.1.0 \
    && pip --no-cache-dir install git+https://github.com/rwightman/pytorch-image-models.git \
    && pip --no-cache-dir install albumentations==1.2.0 \
    && pip --no-cache-dir install opencv-contrib-python-headless==4.5.3.56 \
    && pip --no-cache-dir install opencv-python==4.5.3.56 \
    && pip --no-cache-dir install gdown==4.4.0 \
    && pip --no-cache-dir install hungarian_algorithm \
    && pip --no-cache-dir install onnxruntime-gpu==1.11 \
    && pip --no-cache-dir install transformers \
    && pip --no-cache-dir install ordereddict==1.1 \
    # >>> Install mmcv-full: (https://mmcv.readthedocs.io/en/latest/get_started/installation.html)
    && pip --no-cache-dir install mmcv-full==1.6.0 -f https://download.openmmlab.com/mmcv/dist/cu113/torch1.11.0/index.html \
    # && pip --no-cache-dir install mmsegmentation \
    # && pip --no-cache-dir install mmdet \
    && pip --no-cache-dir install ensemble_boxes \
    # && pip --no-cache-dir install -U openmim==0.1.6 \
    # >>> Required by Swin Transformer
    && pip --no-cache-dir install onnx==1.12.0 \
    && pip --no-cache-dir install yacs \
    # >>> coco detection dataset
    && pip --no-cache-dir install pycocotools==2.0.4 \
    # >>> UMAP and tsne, numpy version can not be too high because of numba
    && pip --no-cache-dir install numpy==1.22.0 \
    && pip --no-cache-dir install umap-learn==0.5.3 

RUN pip --no-cache-dir install wandb

RUN pip --no-cache-dir install -U sentence-transformers \
    && pip --no-cache-dir install gradio

# calculate FLOPs and Parameter number
RUN pip --no-cache-dir install thop

RUN pip --no-cache-dir install terminaltables

RUN pip --no-cache-dir install effdet

RUN git clone https://github.com/facebookresearch/detectron2 detectron2_repo
RUN pip install -e detectron2_repo

RUN pip --no-cache-dir install seaborn


RUN chmod 777 -R /home/user


# Set the default command to python3
CMD ["python3"]
