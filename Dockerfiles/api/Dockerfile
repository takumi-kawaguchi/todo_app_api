FROM golang:latest

ENV GOPATH /go
ENV PATH $PATH:$GOPATH/bin

ENV GO111MODULE=on
ENV PORT=1323

RUN mkdir -p /go/src/api
COPY . /go/src/api
WORKDIR /go/src/api

RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    && apt-get -y install git openssh-client less iproute2 procps lsb-release \
    && mkdir -p /tmp/gotools \
    && cd /tmp/gotools \
    # get gopls
    && GOPATH=/tmp/gotools GO111MODULE=on go get -v golang.org/x/tools/gopls@latest 2>&1 \
    # get each go lib
    && GOPATH=/tmp/gotools GO111MODULE=on go get -v \
    honnef.co/go/tools/...@latest \
    golang.org/x/tools/cmd/gorename@latest \
    golang.org/x/tools/cmd/goimports@latest \
    golang.org/x/tools/cmd/guru@latest \
    golang.org/x/lint/golint@latest \
    github.com/mdempsky/gocode@latest \
    github.com/cweill/gotests/...@latest \
    github.com/haya14busa/goplay/cmd/goplay@latest \
    github.com/sqs/goreturns@latest \
    github.com/josharian/impl@latest \
    github.com/davidrjenni/reftools/cmd/fillstruct@latest \
    github.com/uudashr/gopkgs/v2/cmd/gopkgs@latest  \
    github.com/ramya-rao-a/go-outline@latest  \
    github.com/acroca/go-symbols@latest  \
    github.com/godoctor/godoctor@latest  \
    github.com/rogpeppe/godef@latest  \
    github.com/zmb3/gogetdoc@latest \
    github.com/fatih/gomodifytags@latest  \
    github.com/mgechev/revive@latest  \
    github.com/go-delve/delve/cmd/dlv@latest 2>&1 \
    github.com/go-sql-driver/mysql \
    github.com/google/uuid \
    github.com/gorilla/mux \
    # # get gomod
    # && GOPATH=/tmp/gotools go get -x -d github.com/stamblerre/gocode 2>&1 \
    # && GOPATH=/tmp/gotools go build -o gocode-gomod github.com/stamblerre/gocode \
    # Install Go tools
    && mv /tmp/gotools/bin/* /usr/local/bin/
# && mv gocode-gomod /usr/local/bin/

ENV PORT=1324