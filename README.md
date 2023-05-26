# Get release or tag

[![Action test on Ubuntu](https://github.com/GuillaumeFalourd/get-release-or-tag/actions/workflows/ubuntu_action_test.yml/badge.svg)](https://github.com/GuillaumeFalourd/get-release-or-tag/actions/workflows/ubuntu_action_test.yml) [![Action test on MacOs](https://github.com/GuillaumeFalourd/get-release-or-tag/actions/workflows/macos_action_test.yml/badge.svg)](https://github.com/GuillaumeFalourd/get-release-or-tag/actions/workflows/macos_action_test.yml) [![Action test on Windows](https://github.com/GuillaumeFalourd/get-release-or-tag/actions/workflows/windows_action_test.yml/badge.svg)](https://github.com/GuillaumeFalourd/get-release-or-tag/actions/workflows/windows_action_test.yml)

Github action to get release or tag (SHA).

**Supported runners**: `ubuntu`, `macos`, `windows`

## Usage

[![Public workflows that use this action.](https://img.shields.io/endpoint?url=https%3A%2F%2Fapi-endbug.vercel.app%2Fapi%2Fgithub-actions%2Fused-by%3Faction%3DGuillaumeFalourd%2Fget-release-or-tag%26badge%3Dtrue)](https://github.com/search?o=desc&q=GuillaumeFalourd+get-release-or-tag+path%3A.github%2Fworkflows+language%3AYAML&s=&type=Code)

### Basic

```
steps:
   - uses: actions/checkout@v3

   - id: tag
     uses: GuillaumeFalourd/get-release-or-tag@v2

   - name: TAG
     run: echo "TAG ${{ steps.tag.outputs.tag }}"
```

### With Docker images

This action can for example helps you get release docker images in a dev/prod pipeline. 
It will return the release name (`$GITHUB_REF` without `refs/tags/`) if the action is `release` otherwise it will return `$GITHUB_SHA`

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
      - uses: actions/checkout@v3

      - uses: GuillaumeFalourd/get-release-or-tag@v2
        id: tag

      - name: Build
        run: docker build src/flyway -t your.docker.repo/flyway:${{ steps.tag.outputs.tag }}

      - name: Push
        run: docker push your.docker.repo/flyway:${{ steps.tag.outputs.tag }}
```

## Action Outputs

Field | How to access | Observation
------------ | ------------  | -------------
**tag** | `${{ steps.<step-id>.outputs.tag }}` | Contains last release tag or SHA

* * *

## 🤝 Contributing

☞ [Guidelines](https://github.com/GuillaumeFalourd/get-release-or-tag/blob/master/CONTRIBUTING.md)

## 🏅 Licensed

☞ This repository uses the [Apache License 2.0](https://github.com/GuillaumeFalourd/get-release-or-tag/blob/master/LICENSE)
