FROM kalilinux/kali-rolling:latest
ENV DEBIAN_FRONTEND=noninteractive

# 0. essentials + non-root user that can sudo without password
RUN apt-get update && apt-get -y dist-upgrade && \
    apt-get install -y --no-install-recommends \
        sudo git curl vim nano zsh wget ca-certificates gnupg2 \
        apt-transport-https software-properties-common && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

ARG USERNAME=kali
ARG USER_UID=1001
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME && \
    useradd --uid $USER_UID --gid $USER_GID -m -s /bin/zsh $USERNAME && \
    echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

# 1. switch default shell
RUN chsh -s /bin/zsh root && chsh -s /bin/zsh $USERNAME
CMD [ "/bin/zsh" ]