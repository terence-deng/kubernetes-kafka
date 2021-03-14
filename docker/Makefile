VERSION=1.0-2.6.1
PROJECT_ID=kubernetes-kafka
PROJECT=terencedeng

all: build

build:
	docker build --pull -t ${PROJECT}/${PROJECT_ID}:${VERSION} .

push: build
	docker push ${PROJECT}/${PROJECT_ID}:${VERSION}

.PHONY: all build push
