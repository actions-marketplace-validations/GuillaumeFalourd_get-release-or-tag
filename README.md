# Get release name or tag

Github action to get release name and tag.

**Supported runners**: `ubuntu-latest`

## Usage

### Basic

```
steps:
   - id: tag
     uses: GuillaumeFalourd/get-release-or-tag@v1

   - name: TAG
     run: echo "TAG ${{ steps.tag.outputs.tag }}"
```

### With Docker images

This action can for example helps you get release docker images in a dev/prod pipeline. It will return the release name (`$GITHUB_REF` without `refs/tags/`) if the action is `release` otherwise it will return `$GITHUB_SHA`

Ex:

```
name: Publish

on:
  release:
    types:
      - published

jobs:
  build_docker_image:
    name: Flyway
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: GuillaumeFalourd/get-release-or-tag@v1
        id: tag

      - name: Build
        run: docker build src/flyway -t your.docker.repo/flyway:${{ steps.tag.outputs.tag }}

      - name: Push
        run: docker push your.docker.repo/flyway:${{ steps.tag.outputs.tag }}
```

## Action Outputs

Field | How to access | Observation
------------ | ------------  | ------------- | -------------
**tag** | `${{ steps.<step-id>.outputs.tag }}` | Contains last release tag

* * *

## 🤝 Contributing

☞ [Guidelines](https://github.com/GuillaumeFalourd/get-release-or-tag/blob/master/CONTRIBUTING.md)

## 🏅 Licensed

☞ This repository uses the [Apache License 2.0](https://github.com/GuillaumeFalourd/get-release-or-tag/blob/master/LICENSE)
