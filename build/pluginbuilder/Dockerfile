## Copyright 2018 The Nakama Authors
##
## Licensed under the Apache License, Version 2.0 (the "License");
## you may not use this file except in compliance with the License.
## You may obtain a copy of the License at
##
## http://www.apache.org/licenses/LICENSE-2.0
##
## Unless required by applicable law or agreed to in writing, software
## distributed under the License is distributed on an "AS IS" BASIS,
## WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
## See the License for the specific language governing permissions and
## limitations under the License.

# docker build . --file ./Dockerfile --build-arg version=v2.1.1 -t heroiclabs/nakama-pluginbuilder:2.1.1
# docker build . --file ./Dockerfile --build-arg version="v2.1.1-$(git rev-parse --short HEAD)" -t heroiclabs/nakama-pluginbuilder:"2.1.1-$(git rev-parse --short HEAD)"

FROM golang:1.24.5-bookworm AS builder

ARG VERSION
ARG TARGETOS
ARG TARGETARCH

LABEL maintainer="Heroic Labs"
LABEL contact="support@heroiclabs.com"
LABEL version=$VERSION
LABEL variant=nakama-pluginbuilder
LABEL description="A support container to build Go code for Nakama server's runtime."

ENV GOOS=$TARGETOS
ENV GOARCH=$TARGETARCH
ENV CGO_ENABLED=1
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y --no-install-recommends ca-certificates gcc libc6-dev git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /builder

ENTRYPOINT ["go"]
