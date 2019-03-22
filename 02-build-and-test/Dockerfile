# start from an upstream, maintained build image for Go
FROM golang:1.10

# Install dep (for managing versioned go package dependencies)
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

# create the location for our code, and go there
RUN mkdir -p /go/src/github.com/cevoaustralia/utcservice
WORKDIR /go/src/github.com/cevoaustralia/utcservice

# Copy our code into the work directory
ADD *.go Gopkg* /go/src/github.com/cevoaustralia/utcservice/

# Make sure we have the correct versioned dependencies installed
RUN dep ensure

# Actually run the tests, and then build the binary if the tests passed
RUN go test && go build
