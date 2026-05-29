FROM debian:bullseye-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
        wget bzip2 ca-certificates \
        libglib2.0-0 git \
    && rm -rf /var/lib/apt/lists/*

# Install pixi
RUN wget -q https://github.com/prefix-dev/pixi/releases/latest/download/pixi-x86_64-unknown-linux-musl \
        -O /usr/local/bin/pixi \
    && chmod +x /usr/local/bin/pixi

COPY pixi.toml /benchmark/pixi.toml
# COPY pixi.lock /benchmark/pixi.lock

WORKDIR /benchmark

RUN pixi install

ENV PATH="/benchmark/.pixi/envs/default/bin:$PATH"