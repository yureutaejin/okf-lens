# ubuntu:noble-20260917 multi-architecture image digest
FROM docker.io/library/ubuntu:noble AS base

# MARK: Arguments and Environment Variables
ARG TARGETOS
ARG TARGETARCH
ARG USERNAME=vscode
ARG USER_UID=1001
ARG USER_GID=${USER_UID}

ENV DEBIAN_FRONTEND=noninteractive

# MARK: Common Dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    bash-completion \
    ca-certificates \
    curl \
    git \
    jq \
    ripgrep \
    vim \
    sudo \
    openssh-client \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /etc/ssh /etc/sudoers.d

RUN echo 'github.com ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOMqqnkVzrm0SdG6UOoqKLsabgH5C9okWi0dh2l9GKJl' \
    >> /etc/ssh/ssh_known_hosts

RUN <<EOF
    groupadd --gid ${USER_GID} ${USERNAME}
    useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} --shell /bin/bash
    echo "${USERNAME} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${USERNAME}
    chmod 0440 /etc/sudoers.d/${USERNAME}
EOF

ARG DENO_VERSION=2.7.0
# MARK: Install Deno
RUN <<EOF
    set -e
    case "${TARGETARCH}" in \
        amd64) deno_arch=x86_64 ;; \
        arm64) deno_arch=aarch64 ;; \
        *) echo "Unsupported Deno architecture: ${TARGETARCH}" >&2; exit 1 ;; \
    esac
    curl -fsSL \
        -o /tmp/deno.zip \
        "https://github.com/denoland/deno/releases/download/v${DENO_VERSION}/deno-${deno_arch}-unknown-linux-gnu.zip"
    unzip -q /tmp/deno.zip -d /usr/local/bin
    rm /tmp/deno.zip
    chmod +x /usr/local/bin/deno
EOF

# MARK: Install user preferences
# List:
# - github.com/astral-sh/starship: A cross-shell prompt made with Rust
# - github.com/microsoft/apm: Agent Package Manager
RUN curl -fsSL \
    https://github.com/starship/starship/releases/download/v1.26.0/starship-$(uname -m)-unknown-linux-musl.tar.gz \
    | tar xz -C /usr/local/bin \
    && echo 'eval "$(/usr/local/bin/starship init bash)"' >> /etc/bash.bashrc

RUN <<EOF
  curl -fsSL https://github.com/microsoft/apm/releases/latest/download/apm-linux-${TARGETARCH}.tar.gz | tar -xz -C /usr/local/lib/
  mv /usr/local/lib/apm-${TARGETOS}-${TARGETARCH} /usr/local/lib/apm
  ln -sf /usr/local/lib/apm/apm /usr/local/bin/apm
EOF
