# Blog post: Docker pipeline as code

This repository goes alongside the blog post [Docker multistage builds: a minimal pipeline-as-code](https://cevo.com.au/post/2018-10-29-docker-a-minimal-pipeline-as-code/)

It contains a number of subdirectories:

1. An "01-initial" directory, which contains an example of how you might begin: a `Makefile`
   which builds a Go binary and then packages it into a Docker image for later use. You don't
   _have_ to use `make` for this, it's just an assistant.

   Of course, this requires that you have Go installed, and all the other
   relevant dependencies, and that they're all of an appropriate version.

1. An "02-build-and-test" directory, which contains an example of how you could bundle the
   build-test-package process into a single Docker image, removing the reliance on
   having the right version of Go and so forth installed.

   The resulting image has the service binary, plus all the build-time dependencies, and is
   quite large.

1. An "03-build-test-runtime" directory, which extends the build-and-test Dockerfile
   and creates a working Docker image with the built binary ready to go, in a
   minimal-sized final image

1. An "04-complete" directory, which demonstrates combining multiple Docker images
   into a single, minimised final image
