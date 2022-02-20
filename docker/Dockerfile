ARG PYTORCH="1.10.0"
ARG CUDA="11.3"
ARG CUDNN="8"

FROM pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel

ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install pytorch-openpose
RUN apt update && apt install -y git libopencv-dev  \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/Hzzone/pytorch-openpose.git /pytorch-openpose
WORKDIR /pytorch-openpose
RUN pip install -r requirements.txt

RUN mkdir -p /pytorch-openpose/model

# add user
ARG USERNAME=takuser
ARG GROUPNAME=takuser
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID $USERNAME

RUN chown -R takuser:takuser /pytorch-openpose
USER $USERNAME
