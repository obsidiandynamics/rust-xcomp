FROM rust:1.65.0-slim-bullseye

RUN apt-get update \
    && apt-get install -y \
        bash \
        curl \
        g++ \
        gcc \
        git \
        jq \
        libsasl2-dev \
        libssl-dev \
        libxml2-dev \
        libz-dev \
        xz-utils \
        zip

COPY MacOSX12.3.sdk.tar.xz /opt

# Darwin linker
RUN apt install -y clang cmake \
    && cd /opt \
    && git clone https://github.com/tpoechtrager/osxcross \
    && cd osxcross \
    && mv ../MacOSX12.3.sdk.tar.xz tarballs/ \
    && UNATTENDED=yes OSX_VERSION_MIN=12.3 ./build.sh \
    && rm tarballs/*

ENV PATH="/opt/osxcross/target/bin:$PATH"
ENV CARGO_TARGET_X86_64_APPLE_DARWIN_LINKER=x86_64-apple-darwin21.4-clang
ENV CARGO_TARGET_AARCH64_APPLE_DARWIN_LINKER=aarch64-apple-darwin21.4-clang

# Windows linker
RUN apt install -y mingw-w64

# Rust extensions pre-installed for faster builds
RUN cargo install cargo2junit cargo-get cargo-criterion grcov \
    && rustup component add rust-src rustfmt clippy llvm-tools-preview \
    && rustup toolchain install nightly

# Additional targets for multiarch builds
RUN rustup target install \
    x86_64-pc-windows-gnu \
    x86_64-apple-darwin \
    aarch64-apple-darwin