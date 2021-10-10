# start from an upstream, maintained build image for Go
FROM golang:1.16.8

ARG VERSION=0.1

# create the location for our code, and go there
RUN mkdir /build
WORKDIR /build

# Fetch the appropriate version
RUN curl -L -s https://github.com/cevoaustralia/utcservice/archive/${VERSION}.tar.gz | tar zxvf -
WORKDIR /build/utcservice-${VERSION}

# Actually run the tests, and then build the binary if the tests passed
RUN go test && go build
