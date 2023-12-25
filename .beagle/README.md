# debian

## build

```bash
sudo podman run -it --rm \
-v $PWD/:$PWD/ \
-w $PWD/ \
--privileged \
registry.cn-qingdao.aliyuncs.com/wod/debian:bookworm \
bash -c '
apt update -y && \
apt install -y xz-utils wget curl debian-ports-archive-keyring debootstrap git && \
mkdir -p .tmp && \
export PATH=$PWD/scripts:$PATH && \
git apply .beagle/loong64.patch && \
./examples/debian.sh --arch loong64 --ports .tmp sid 2023-12-24T00:00:00Z && \
git apply -R .beagle/loong64.patch && \
'

docker build \
-f .beagle/Dockerfile \
-t registry.cn-qingdao.aliyuncs.com/wod/debian:bookworm-loong64 \
./.tmp/20231224/loong64/sid/ \
--load

docker run -it --rm \
-v $PWD/:$PWD/ \
-w $PWD/ \
registry.cn-qingdao.aliyuncs.com/wod/debian:bookworm-loong64 \
bash
```

## git

<https://github.com/debuerreotype/debuerreotype>

```bash
git remote add upstream git@github.com:debuerreotype/debuerreotype.git

git fetch upstream

git merge 0.15
```
