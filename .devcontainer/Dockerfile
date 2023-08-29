FROM condaforge/mambaforge:23.1.0-4

# Default powerline10k theme, no plugins installed
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.5/zsh-in-docker.sh)" -- \
        -p compleat \
        -p git \
        -p gitfast \
        -p zsh-syntax-highlighting

WORKDIR /root/
RUN chsh -s /bin/zsh

RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
    .oh-my-zsh/custom/plugins/zsh-syntax-highlighting

RUN git clone --depth 1 https://github.com/junegunn/fzf.git .fzf
RUN .fzf/install

COPY .devcontainer/.p10k.zsh .
COPY .devcontainer/.zshrc .

# COPY environment.yml .
# RUN mamba env create -f environment.yml
RUN mamba install conda-lock
COPY conda-lock.yml .
RUN conda-lock install -n dev conda-lock.yml

ENTRYPOINT zsh
