FROM golang:1.14.2

LABEL maintainer="LitmusChaos"

RUN apt-get update && apt-get install -y git && \
    apt-get install -y ssh && \
    apt install ssh rsync

ARG KUBECTL_VERSION=1.18.0

#setup go envs
ENV GO111MODULE=off
ENV GOPATH=$HOME/go
ENV PATH=$PATH:/usr/local/go/bin:$GOPATH/bin

#Installing helm
RUN git clone https://github.com/helm/helm.git &&\
    cd helm && make

#Install kubectl
ADD https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl

#copying binaries
COPY build/_output ./

#overwrite entrypoint with test binary
ENTRYPOINT ["./all-experiments"]
