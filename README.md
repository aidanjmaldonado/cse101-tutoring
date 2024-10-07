# Hello!

I'm Aidan Maldonado, a third year computer science major, and I'm excited to be your tutor for Cse 101 Introduction to Data Structures and Algorithms.
My goal with this repository is to provide you all with resources to help apply the concepts we go over in sections and serve as a technical referrence.

**Index** 

* [Setup](#setup)
   * [Clone Repository](#clone-repository)
   * [Docker Setup](#docker-setup)
       * [Dependences](#dependencies)
           * [Software](#software)
           * [Extensions](#extensions)
           * [Docker Files](#docker-files)
               * [.devcontainer/](#devcontainer)
               * [devcontainer.json](#devcontainerjson)
               * [Dockerfile](#dockerfile)
* [Week 2 - Introduction to Abstract Data Types](#week-2)

---
# Setup
## Clone repository
Navigate to a folder within your computer where you'd like to clone this repository. Once you find a spot, in your terminal, run **one** of these two commands:

1. Run this command if you'd like to clone the repository **with** my [Docker files](#docker-packages) pre-installed
```
git clone -b main https://github.com/aidanjmaldonado/cse101-tutoring.git
```
2. Or, run this command if you'd like to clone the repository **without them**, and either [create them your own](#docker-files) or use something other than Docker:
```
git clone -b without-devcontainer https://github.com/aidanjmaldonado/cse101-tutoring.git
```
From here, change directory to work inside the space:
```
cd cse101-tutoring
```

## Docker Setup
While you may be using a different environment to code during your classes such as WSL, VM, Ubuntu, or others, I will provide a brief kickstart guide to navigate setting up a docker environment, which will allow you to write/run C/C++ code, specifically with Visual Studio Code.

### Dependencies
#### Software
1. If you do not have **Visual Studio Code** installed, you may download it from [here](https://code.visualstudio.com/download).
2. If you do not have **Docker Desktop** installed, you may download it from [here](https://www.docker.com/products/docker-desktop/).

#### Extensions
1. Upon opening Visual Studio Code, look for the **Extensions** tab in the left column (or press ```CMD+Shift+X``` on Mac/```CTRL+Shift+X``` on Windows).
2. Search for the extension **Dev Containers** by Microsoft (refer [here](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) to make sure you're downloading the right one).
3. Click "Install"

#### Docker Files
You will need two files to build your Docker Environment.
1. ~/cse101-tutoring/.devcontainer/**devcontainer.json**
2. ~/cse101-tutoring/.devcontainer/**Dockerfile**

##### .devcontainer/
Both ```devcontainer.json``` and ```Dockerfile``` should be placed inside a folder called ```.devcontainer``` in the root directory of your repository (this would be```cse101-tutoring``` in the case of this repository, so it should appear as ```cse101-tutoring/.devcontainer```). You can create the ```.devcontainer``` folder with the following command:
```
mkdir .devcontainer
```
##### devcontainer.json
This file holds the container's configuration settings, such as which ```Dockerfile``` (see below) to use, settings, extensions, and post-creation commands. You can create and open your ```devcontainer.json``` with the following command:
```
code .devcontainer/devcontainer.json
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


##### Dockerfile
This file will tell your Docker environment which packages to install upon being built, such as git, vim, valgrind, clang, lldb, etc, and should also go inside the ```.devcontainer/``` directory. So, after creating the ```devcontainer.json```, you can create and open the ```Dockerfile``` with:
```
code .devcontainer/Dockerfile
```
Here is an example of what will go inside your ```Dockerfile```, though you may also customize this to suit your needs:
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

#### Reopen in Docker
Now that all the files are set up, the last thing to do is build the environment. To utilize the ```Dev Containers``` extension, press ```CMD+Shift+P``` (Mac) or ```CTRL+Shift+P``` (Windows) and look for
```
>Dev Containers: Open Folder in Container
```
Click this, then search for the ```cse101-tutoring``` directory and click that to reopen remotely with your Docker.

#### All finished!
Now, in the bottom left, you should see ```Dev Container: CSE 101 Tutoring @ desktop-linux```, and you can check whether the build was successful by checking various packages.
For instance, if you run
```
clang
```
in your terminal, you should be met with
```
clang: error: no input files
```
and not
```
zsh: command not found: clang
```
To shut down the Docker, in the app look for ```Quick Docker Desktop``` in the app. Reopenning the app should reactivate your environment, but if it does not, power it on from the desktop app.

---

# Week 2
## Introduction to Abstract Data Types