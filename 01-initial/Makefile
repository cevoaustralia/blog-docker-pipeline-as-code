VERSION=0.1
SOURCE=https://github.com/cevoaustralia/utcservice/archive/$(VERSION).tar.gz

all: build image clean

image: build
	cp utcservice-$(VERSION)/utcservice .
	docker build -t utcservice:initial .

build: test
	cd utcservice-$(VERSION) && go build

test: fetch
	cd utcservice-$(VERSION) && go test

fetch:
	curl -L -s $(SOURCE) | tar zxvf -

clean:
	rm -rf utcservice utcservice-$(VERSION)
