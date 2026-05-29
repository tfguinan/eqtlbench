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

RUN pixi install && pixi run install-PCAForQTL

ENV PATH="/benchmark/.pixi/envs/default/bin:$PATH"

# Install SAIGE-QTL from pre-built binary
RUN git clone https://github.com/weizhou0/SAIGEQTL.git /opt/SAIGEQTL \
    && cd /opt/SAIGEQTL \
    && BINARY_FILE=$(ls binaries/SAIGEQTL_*_linux-x86_64.tgz | head -n1) \
    && echo "Installing: $BINARY_FILE" \
    && CONDA_OVERRIDE_GLIBC=2.28 pixi run R -e " \
        install.packages('${BINARY_FILE}', repos = NULL, type = 'source') ; \
        library(SAIGEQTL) ; \
        cat('SAIGEQTL', as.character(packageVersion('SAIGEQTL')), 'installed\n') \
    "

ENV PATH="/opt/SAIGEQTL/extdata:${PATH}"