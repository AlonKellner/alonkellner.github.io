FROM mcr.microsoft.com/devcontainers/jekyll

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y ffmpeg sox libavdevice-dev python3 python3-pip

COPY requirements.txt requirements.txt
RUN --mount=type=cache,target=/root/.cache/ \
    pip install -r requirements.txt --break-system-packages
