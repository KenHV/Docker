FROM ubuntu:groovy
LABEL maintainer="KenHV <kenhv@null.net>"
RUN apt-get update -qq && \
    apt-get install --no-install-recommends -y -qq \
        bc \
        bison \
        ca-certificates \
        curl \
        flex \
        gcc \
        git \
        libc6-dev \
        libssl-dev \
        make \
        openssh-client \
        python3-minimal \
        zip && \
    apt-get autoremove -y && \
    apt-get clean autoclean && \
    rm -rf /var/lib/apt/lists/*
RUN git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9 \
    --depth=1 /root/toolchains/aarch64
RUN git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-eabi-4.8 \
    --depth=1 /root/toolchains/aarch32
RUN git clone https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86 \
    --depth=1 /root/toolchains/clang
RUN git config --global user.email "kenhv@null.net"
RUN git config --global user.name "KenHV"
