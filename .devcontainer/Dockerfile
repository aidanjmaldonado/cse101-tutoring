# Use the official Ubuntu image as a base
FROM ubuntu:20.04

# Set up non-interactive frontend for apt-get
ENV DEBIAN_FRONTEND=noninteractive

# Clean up apt cache to reduce image size
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install basic dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    gdb \
    clang \
    clang-format \
    clang-tidy \
    valgrind \
    git \
    vim \
    lldb \
    python3 \
    python3-pip \
    python3-venv

# Set up a user for vscode
ARG USERNAME=vscode
RUN useradd -m ${USERNAME} && echo "${USERNAME}:password" | chpasswd && adduser ${USERNAME} sudo

# Set the default user to vscode
USER ${USERNAME}

# Set the working directory
WORKDIR /workspaces