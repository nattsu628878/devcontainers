FROM ubuntu

ARG HOST_PWD
WORKDIR $HOST_PWD

SHELL ["bash", "-c"]

# install basic packages
RUN apt update \
  && apt install -y \
    curl \
    git \
    build-essential

# set up git
RUN git config --global user.name nattsu628878 \
  && git config --global user.email natsuichi0817@gmail.com \
  && git config --global init.defaultBranch main \
  && git config --global pull.rebase false

# install docker cli
RUN install -m 0755 -d /etc/apt/keyrings \
  && curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc \
  && chmod a+r /etc/apt/keyrings/docker.asc \
  && echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null \
  && apt update \
  && apt install -y docker-ce-cli

# install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH="/root/.cargo/bin:${PATH}"

CMD ["bash"]
