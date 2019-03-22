# start from an upstream, maintained build image for Go
# This time, we're giving it a friendly name for use later in the pipeline
FROM golang:1.10 AS build

# Install dep (for managing versioned go package dependencies)
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

# create the location for our code, and go there
RUN mkdir -p /go/src/github.com/cevoaustralia/utcservice
WORKDIR /go/src/github.com/cevoaustralia/utcservice

# Copy our code into the work directory
ADD *.go Gopkg* /go/src/github.com/cevoaustralia/utcservice/

# Make sure we have the correct versioned dependencies installed
RUN dep ensure

# Actually run the tests, and then build a statically-linked binary if the tests passed
RUN go test && \
	CGO_ENABLED=0 GOOS=linux go build -a -ldflags '-extldflags "-static"'

# This is the second stage -- starting from the most minimal possible image
FROM scratch

# We copy in the built binary from the previous stage
COPY --from=build /go/src/github.com/cevoaustralia/utcservice/utcservice /

# and away we go
EXPOSE 8080
ENTRYPOINT ["/utcservice"]
