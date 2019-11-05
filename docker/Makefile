.DEFAULT_GOAL := help
.PHONY: help

UID=$(id -u)
GID=$(id -g)

build: ## build -t docker-gpu-test:latest
	docker build -t docker-gpu-test:latest .

xhost-setup:
	xhost +local:root

test-smi: ## docker-gpu-test:latest nvidia-smi
	docker run --rm --gpus all docker-gpu-test:latest nvidia-smi

test-bash: ## docker-gpu-test:latest bash
	docker run -it --rm --gpus all -e DISPLAY=:0 -v /tmp/.X11-unix/:/tmp/.X11-unix docker-gpu-test:latest bash

test-bash-nogpu: ## docker-gpu-test:latest bash
	docker run -it --rm -e DISPLAY=:0 -v /tmp/.X11-unix/:/tmp/.X11-unix docker-gpu-test:latest bash

ubuntu-cuda-smi: ## nvidia/cuda:10.1-base-ubuntu18.04 nvidia-smi
	docker run --rm --gpus all nvidia/cuda:10.1-base-ubuntu18.04 nvidia-smi

debian-smi: ## debian nvidia-smi
	docker run --rm --gpus all debian nvidia-smi

ubuntu-smi: ## ubuntu nvidia-smi
	docker run --rm --gpus all ubuntu nvidia-smi
help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

