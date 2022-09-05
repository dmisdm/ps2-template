# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.241.1/containers/python-3/.devcontainer/base.Dockerfile

# [Choice] Python version (use -bullseye variants on local arm64/Apple Silicon): 3, 3.10, 3.9, 3.8, 3.7, 3.6, 3-bullseye, 3.10-bullseye, 3.9-bullseye, 3.8-bullseye, 3.7-bullseye, 3.6-bullseye, 3-buster, 3.10-buster, 3.9-buster, 3.8-buster, 3.7-buster, 3.6-buster
ARG VARIANT="3.10-bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/python:0-${VARIANT}

# [Choice] Node.js version: none, lts/*, 16, 14, 12, 10
ARG NODE_VERSION="none"
RUN if [ "${NODE_VERSION}" != "none" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi


COPY ./.devcontainer/MinecraftToolsLinux.zip .
ADD https://github.com/rmit-computing-technologies/COSC2804-project-template-TEST/releases/download/jdk-15/jdk-15.0.2_linux-x64_bin.deb .
COPY ./.devcontainer/start_server.sh .

RUN unzip MinecraftToolsLinux.zip
RUN mv /Minecraft\ Tools /MinecraftTools
RUN chmod -R 777 /MinecraftTools
RUN chmod +x /MinecraftTools/Install_API.sh
RUN chmod +x /MinecraftTools/start_server.sh

RUN cd /MinecraftTools && ./Install_API.sh

RUN apt-get -y update

RUN apt install -y ./jdk-15.0.2_linux-x64_bin.deb
ENV JAVA_HOME=/usr/lib/jvm/jdk-15.0.2
ENV PATH=$PATH:$JAVA_HOME/bin


RUN chmod +x /start_server.sh

# RUN chmod +x ./MinecraftToolsLinux/Install_API
# RUN ./MinecraftToolsLinux/Install_API

# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
# COPY requirements.txt /tmp/pip-tmp/
# RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
#    && rm -rf /tmp/pip-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1