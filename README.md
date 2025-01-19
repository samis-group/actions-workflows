# Reusable Actions Workflows

This is where I store all of my reusable github actions workflows.

## Build and publish docker image to ghcr.io

### Inputs

#### Required Inputs

- **image_name**: Name of the image

#### Optional Inputs

- **registry**: The registry to use for hosting the images (default: 'ghcr.io')
- **dockerfile**: The folder where the image is built from (default: './Dockerfile')
- **context_dir**: The folder where the image is built from (default: '.')
- **build_contexts**: The named build contexts to use (default: '')
- **platforms**: The architecture to build the image for (default: 'linux/amd64')
- **build_target**: The target at which to build the image (default: '')
- **run_on_runners**: The Runners that build and publish the image (default: 'self-hosted')

### Example

Mkdocs base:

```yaml
name: Docker Image - mkdocs-base

on:
  push:
    paths:
      - "assets/**"
      - "Dockerfile"
    branches:
      - 'main'
  workflow_dispatch:
  pull_request:
    branches:
      - 'main'

jobs:
  build:
    uses: samis-group/actions-workflows/.github/workflows/docker-build-and-publish.yaml@main
    with:
      image_name: mkdocs-base
```

An example with multiple named contexts:

```yaml
name: Docker Image - Workstation

on:
  push:
    paths:
      - 'docker/workstation/**'
      - 'provision/ansible/requirements.yml'
      - 'provision/ansible/roles/requirements.yml'
      - 'requirements.txt'
    branches:
      - 'main'
  workflow_dispatch:
  pull_request:
    branches:
      - 'main'

jobs:
  build:
    uses: samis-group/actions-workflows/.github/workflows/docker-build-and-publish.yaml@main
    with:
      image_name: workstation
      platforms: 'linux/amd64,linux/arm64'
      dockerfile: docker/workstation/Dockerfile
      # run_on_runners: "ubuntu-latest" # Use public runner for public project if you would like
      build_contexts: |
        project=./
        dockerdir=docker/workstation
```
