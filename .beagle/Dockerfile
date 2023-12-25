FROM scratch
ADD rootfs.tar.xz /
RUN sed -i 's/http\:\/\/deb.debian.org/http\:\/\/mirrors.aliyun.com/g' /etc/apt/sources.list.d/debian.sources && \
  apt update -y && DEBIAN_FRONTEND=noninteractive apt install ca-certificates -y && \
  sed -i 's/http\:\/\/mirrors.aliyun.com/https\:\/\/mirrors.aliyun.com/g' /etc/apt/sources.list.d/debian.sources && \
  cat /etc/apt/sources.list.d/debian.sources && \
  apt-get clean && \
  rm -rf /etc/localtime && \
  ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
CMD ["bash"]