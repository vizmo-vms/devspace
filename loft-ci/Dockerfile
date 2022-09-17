FROM alpine:3 as alpine

ARG DEVSPACE_RELEASE_VERSION=v6.1.1
ARG LOFT_RELEASE_VERSION=v2.3.0
ARG DOCKER_BUILDX_VERSION=v0.9.1

RUN apk add --update-cache curl tar docker git

RUN curl -L -o /bin/kubectl https://storage.googleapis.com/kubernetes-release/release/v1.23.10/bin/linux/amd64/kubectl \
  && chmod +x /bin/kubectl

RUN wget -O helm.tar.gz https://get.helm.sh/helm-v3.3.3-linux-amd64.tar.gz \
  && tar -zxvf helm.tar.gz \
  && mv linux-amd64/helm /bin/helm

RUN mkdir -p /root/.docker/cli-plugins \
  && curl -L -o docker-buildx https://github.com/docker/buildx/releases/download/$DOCKER_BUILDX_VERSION/buildx-$DOCKER_BUILDX_VERSION.linux-amd64 \
  && chmod +x docker-buildx \
  && mv docker-buildx /root/.docker/cli-plugins/
  
RUN curl -L -o devspace https://github.com/loft-sh/devspace/releases/download/$DEVSPACE_RELEASE_VERSION/devspace-linux-amd64 \
  && chmod +x devspace \
  && mv devspace /bin/devspace

# Add Loft CLI (same version as the tag of this image)
RUN curl -L -o loft https://github.com/loft-sh/loft/releases/download/$LOFT_RELEASE_VERSION/loft-linux-amd64 \
  && chmod +x loft \
  && mv loft /bin/loft
