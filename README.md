# Reusable Actions Workflows

This is where I store all of my reusable github actions workflows.

Example project:

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
