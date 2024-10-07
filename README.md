# Hello!

I'm Aidan Maldonado, I'm a third year computer science major, and I'm excited to be your tutor for Cse 101 Introduction to Data Structures and Algorithms.
My goal with this repository is to provide you all with resources to help apply the concepts we go over in sections and serve as a technical refernce.

---
# Clone repository
Navigate to a folder within your computer where you'd like to clone this repository. In your terminal, run **one** of these two commands:

1. Run this command if you'd like to clone the repository **with** my [Docker files](#docker-packages) pre-installed
```
git clone -b with-devcontainer https://github.com/aidanjmaldonado/cse101-tutoring.git
```
2. Or, run this command if you'd like to clone the repository **without them**, and either create them your own or use something other than Docker:
```
git clone -b without-devcontainer https://github.com/aidanjmaldonado/cse101-tutoring.git
```
From here, change directory to work inside the space:
```
cd cse101-tutoring
```

# Setup
## 1. Docker Environment
While you may be using a different environment to code during your classes such as WSL, VM, Ubuntu, or others, I will provide a brief kickstart guide to establishing a docker environment, which will allow you to write/run C/C++ code, specifically with Visual Studio Code.

### Downloading Dependencies
#### Software
1. If you do not have **Visual Studio Code** installed, you may download it from [here](https://code.visualstudio.com/download).
2. If you do not have **Docker Desktop installed**, you may download it from [here](https://www.docker.com/products/docker-desktop/).

#### Extensions
1. Upon opening Visual Studio Code, look for the **Extensions** tab in the left column (or press ```CMD+Shift+X``` on Mac/```CTRL+Shift+X``` on Windows).
2. Search for the extension "Dev Containers" by Microsoft (refer [here](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) to make sure you're downloading the right one).
3. Click "Install"

### Docker Packages
You will need two files to build your Docker Environment.
1. devcontainer.json
2. Dockerfile
   
#### devcontainer.json
This file holds the container's configuration settings, such as which ```Dockerfile``` (see below) to use, settings, extensions, and post-creation commands.
```devcontainer.json```: This file should be placed inside a folder called ```.devcontainer``` in the root directory of your repository (This would be```cse101-tutoring``` in the case of this repository, so it should appear as cse101-tutoring/.devcontainer). You can create the ```.devcontainer``` folder with the following commands:
```
mkdir .devcontainer
```
```
cd .devcontainer
```
```
code devcontainer.json
```
I prefer VSCode, but use vim/nano or any other text editor you prefer 

Here is an example of what will go inside your ```devcontainer.json```, though you may customize this to suit your needs:
```
{
    "name": "CSE 101 Tutoring",      // To help denote which container you're using, change to match your use case
    "dockerFile": "Dockerfile",      // Points to the Dockerfile in the same folder
    "context": "..",                 // Set this to the directory that contains the `.devcontainer` folder
    "customizations": {
        "vscode": {
            "settings": {
                "editor.defaultFormatter": "ms-vscode.cpptools"
            },
            "extensions": [
                "ms-vscode.cpptools",                   // C++ tools and Intellisense (Comment out/delete if not desired)
                "ms-vscode.cmake-tools",                // CMake support (Comment out/delete if not desired)
                "ms-vscode-remote.remote-containers"    // Dev Containers support (Comment out/delete if not desired)
            ]
        }
    },
    //Comment out/delete the following line to not execute the command after container is build
    "postCreateCommand": "sudo apt-get update && sudo apt-get install -y cmake",

    // Uncomment below to connect as an existing user other than the container default. More info: https://aka.ms/dev-containers-non-root.
    "remoteUser": "vscode", // Change "vscode" to "root" if you want to specify root
    "forwardPorts": []  // Optional list of ports 
}
```


#### Dockerfile
This file will tell your Docker environment which packeges to install upon being built, such as git, vim, valgrind, clang, lldb, etc, and should also go inside the ```.devcontainer folder```. So after creating the ```devcontainer.json```, you can create the ```Dockerfile```:
```
code Dockerfile
```
Here is an example of what will go inside your ```Dockerfile```, though you ma ycustomize this to suit your needs:
```
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
```

### Reopen in Docker
Now that all the files are set up, the last thing to do is build the environment. 
First, step out of the .devcontainers folder with
```
cd..
```
and now, to utilize the ```Dev Containers``` extension, press ```CMD+Shift+P``` (Mac) or ```CTRL+Shift+P``` (Windows) and look for
```
>Dev Containers: Open Folder in Container
```
Click this, then search for the ```cse101-tutoring``` directory and click that to reopen remotely with your Docker.

### All finished!
