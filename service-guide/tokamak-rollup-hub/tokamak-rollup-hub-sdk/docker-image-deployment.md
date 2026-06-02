---
description: Deploy the TRH SDK inside a Docker container to avoid local architecture issues.
---

# Docker Image Deployment

## Overview

The TRH SDK Docker image is a containerized application that lets you interact with the TRH SDK. The image ships with the SDK and its dependencies pre-installed, so you can start deploying immediately after the container is running.

This deployment style is most useful when your local machine architecture is incompatible with native SDK dependencies, or when you prefer an isolated environment.

{% hint style="warning" %}
Docker-based deployment currently supports **Testnet** only.
{% endhint %}

## Prerequisites

* Docker installed — see the [official Docker installation guide](https://docs.docker.com/engine/install/) if needed.

## Getting Started

### 1. Check your machine architecture

```bash
uname -m
```

### 2. Pull the Docker image

Choose the tag that matches your architecture:

**arm64 / aarch64**

```bash
docker pull tokamaknetwork/trh-sdk:itest-reg-arm64
```

**amd64 / x86\_64**

```bash
docker pull tokamaknetwork/trh-sdk:itest-reg-amd64
```

After pulling, verify the image is present:

```bash
docker images
```

You should see a row for `tokamaknetwork/trh-sdk` in the output.

### 3. Run the Docker container

**arm64 / aarch64**

```bash
docker run -d --name trh-sdk-container tokamaknetwork/trh-sdk:itest-reg-arm64 sleep infinity
```

**amd64 / x86\_64**

```bash
docker run -d --name trh-sdk-container tokamaknetwork/trh-sdk:itest-reg-amd64 sleep infinity
```

Verify the container is running:

```bash
docker ps
```

You should see `trh-sdk-container` listed with status `Up`.

### 4. Enter the container

```bash
docker exec -it trh-sdk-container /bin/bash
```

You now have a shell inside the container with the SDK available.

### 5. Verify the SDK version

```bash
trh-sdk version

# expected output
Version: v1.0.1-0.20250825101326-8d221822ba8c
```

{% hint style="warning" %}
**Data persistence:** All chain data is stored inside the container. If you remove the container, that data will be lost. Back up any important chain state before running `docker rm`.
{% endhint %}

## Next Steps

With your Docker environment ready, continue with the SDK setup and deployment steps described in the [Getting Started](getting-started.md) page.
