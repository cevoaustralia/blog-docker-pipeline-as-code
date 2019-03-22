VERSION=0.1

all: clock-image utc-image

clock-image:
	cd clock && docker build -t static-assets:latest .

utc-image:
	docker build --build-arg VERSION=$(VERSION) -t utcservice:with-assets .
