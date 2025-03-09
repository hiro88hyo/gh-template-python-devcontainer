FROM python:3.11-bookworm
USER root

RUN apt update && \
    apt -y install --reinstall ca-certificates && \
    apt -y install software-properties-common && \
    apt -y install git jq && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* && \
    pip install --upgrade pip

RUN curl -s https://api.github.com/repos/cli/cli/releases/latest | jq .assets[].browser_download_url | grep linux_amd64.deb | xargs -I '{}' curl -sL -o /tmp/ghcli.deb '{}' && \
    dpkg -i /tmp/ghcli.deb && \
    rm /tmp/ghcli.deb

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME