
FROM mcr.microsoft.com/devcontainers/base:jammy

ARG DEBIAN_FRONTEND=noninteractive
ARG USER=vscode
ARG USER_UID=1000
ARG USER_GID=1000

RUN DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y build-essential --no-install-recommends make \
        ca-certificates \
        git \
        libssl-dev \
        zlib1g-dev \
        libbz2-dev \
        libreadline-dev \
        libsqlite3-dev \
        curl \
        llvm \
        libncurses5-dev \
        xz-utils \
        tk-dev \
        libxml2-dev \
        libxmlsec1-dev \
        libffi-dev \
        liblzma-dev \
        zsh \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Python + dependencies installation
USER $USER
ARG HOME="/home/$USER"
ENV PYENV_ROOT="${HOME}/.pyenv"
ENV PATH="${PYENV_ROOT}/shims:${PYENV_ROOT}/bin:/${HOME}/.local/bin:$PATH"

WORKDIR ${HOME}

COPY .python-version ${HOME}/

RUN curl https://pyenv.run | bash && \
    pyenv install "$(cat .python-version)" && \
    pyenv global "$(cat .python-version)"

RUN echo "install dependencies" && \
    pip install --upgrade pip && \
    pip install --no-cache-dir \
        dbt-core~=1.10 \
        dbt-duckdb~=1.9 \
        dbt-postgres~=1.9 \
        sqlfluff~=3.4 \
        pre-commit~=4.3 \
        sqlfluff-templater-dbt~=3.4
