# start from an upstream, maintained build image for Go
# This time, we're giving it a friendly name for use later in the pipeline
FROM golang:1.12 AS build

ARG VERSION=0.1

# create the location for our code, and go there
RUN mkdir /build
WORKDIR /build

# Fetch the appropriate version
RUN curl -L -s https://github.com/cevoaustralia/utcservice/archive/${VERSION}.tar.gz | tar zxvf -
WORKDIR /build/utcservice-${VERSION}

# Actually run the tests, and then build a statically-linked binary if the tests passed
RUN go test && \
	CGO_ENABLED=0 GOOS=linux go build -a -ldflags '-extldflags "-static"'

# This is the second stage -- starting from the most minimal possible image
FROM scratch

ARG VERSION=0.1

# We copy in the built binary from the previous stage
COPY --from=build /build/utcservice-${VERSION}/utcservice /

# and away we go
EXPOSE 8080
ENTRYPOINT ["/utcservice"]
