# Build instructions

## Prepare

```sh
mkdir -p build && cd build

curl --proto =https --tlsv1.2 -sSL -o jemalloc_5.3.0.orig.tar.bz2 https://github.com/jemalloc/jemalloc/releases/download/5.3.0/jemalloc-5.3.0.tar.bz2

tar xf jemalloc_5.3.0.orig.tar.bz2
git clone https://github.com/netxms/jemalloc-deb jemalloc-5.3.0/debian
rm -rf jemalloc-5.3.0/debian/.git
```

## PBuilder

```sh
cd jemalloc-5.3.0
ARCH=amd64 DIST=bookworm pdebuild
```

## Docker

```sh
docker run -it --rm -v .:/build -w /build debian:12 bash -l

apt-get update && apt-get install -y debhelper dh-autoreconf

cd jemalloc-5.3.0
dpkg-buildpackage --no-sign
```
