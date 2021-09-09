build: export DOCKER_BUILDKIT = 1
build:
	docker build --build-arg DEVEL=yes -t docker_demo:dev .

requirements/base.txt: requirements/base.in
	docker run --rm -v $(shell pwd)/requirements:/local docker_demo:dev /bin/bash -c \
	  "python -m piptools compile --upgrade --no-annotate --no-header --allow-unsafe --generate-hashes --output-file /local/base.txt /local/base.in"

.PHONY: build
