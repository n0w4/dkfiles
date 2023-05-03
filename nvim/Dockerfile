FROM debian:bullseye

# update and upgrade image
RUN apt update -y && apt upgrade -y

# install some utils
RUN apt install git openssl curl wget build-essential ca-certificates -y 

# install nvim
RUN wget https://github.com/neovim/neovim/releases/download/stable/nvim-linux64.tar.gz -O /opt/nvim-linux64.tar.gz \
    && tar -xvzf /opt/nvim-linux64.tar.gz -C /opt/ \
    && ln -s /opt/nvim-linux64/bin/nvim /usr/bin \
    && mkdir -p ~/.config/nvim

# install rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

# add rust-analyzer as component 
RUN $HOME/.cargo/bin/rustup component add rust-analyzer

# install golang
RUN wget https://go.dev/dl/go1.20.4.linux-amd64.tar.gz -O /opt/go1.20.4.linux-amd64.tar.gz \
    && tar -xvzf /opt/go1.20.4.linux-amd64.tar.gz -C /opt/ 

# install nodejs
RUN wget https://nodejs.org/dist/v20.0.0/node-v20.0.0-linux-x64.tar.xz -O /opt/node-v20.0.0-linux-x64.tar.xz \
    && tar -xf /opt/node-v20.0.0-linux-x64.tar.xz -C /opt/ \
    && ln -s /opt/node-v20.0.0-linux-x64 /opt/nodejs

# setup env PATH
ENV PATH=$HOME/.cargo/bin:/opt/go/bin:/opt/nodejs/bin:$PATH

# configure NVIM plugin manager Packer
RUN git clone --depth 1 https://github.com/wbthomason/packer.nvim\
 ~/.local/share/nvim/site/pack/packer/start/packer.nvim

WORKDIR /workspace
