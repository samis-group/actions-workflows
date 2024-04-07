# Reusable Actions Workflows

This is where I store all of my reusable github actions workflows.

Include them in your project like:

```yaml
jobs:
  build:
    uses: samis-group/actions-workflows/.github/workflows/docker-build-and-publish.yaml@main
    with:
      image_name: actions-runner-base
```
