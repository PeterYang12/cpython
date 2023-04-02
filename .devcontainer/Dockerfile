FROM docker.io/library/fedora:37

ENV CC=clang

ENV WASI_SDK_VERSION=19
ENV WASI_SDK_PATH=/opt/wasi-sdk

ENV WASMTIME_HOME=/opt/wasmtime
ENV WASMTIME_VERSION=7.0.0
ENV WASMTIME_CPU_ARCH=x86_64

RUN dnf -y --nodocs install git clang xz python3-blurb dnf-plugins-core && \
    dnf -y --nodocs builddep python3 && \
    dnf -y clean all

RUN mkdir ${WASI_SDK_PATH} && \
    curl --location https://github.com/WebAssembly/wasi-sdk/releases/download/wasi-sdk-${WASI_SDK_VERSION}/wasi-sdk-${WASI_SDK_VERSION}.0-linux.tar.gz | \
    tar --strip-components 1 --directory ${WASI_SDK_PATH} --extract --gunzip

RUN mkdir --parents ${WASMTIME_HOME} && \
    curl --location "https://github.com/bytecodealliance/wasmtime/releases/download/v${WASMTIME_VERSION}/wasmtime-v${WASMTIME_VERSION}-${WASMTIME_CPU_ARCH}-linux.tar.xz" | \
    xz --decompress | \
    tar --strip-components 1 --directory ${WASMTIME_HOME} -x && \
    ln -s ${WASMTIME_HOME}/wasmtime /usr/local/bin