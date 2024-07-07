# cwnt rust release process

> Workflow to publish a Rust package at crates.io
> [The Cargo Book > Publishing on crates.io](https://doc.rust-lang.org/cargo/reference/publishing.html)

<!-- toc -->

- [Manually](#manually)
- [Automatically (CI/CD)](#automatically-cicd)

<!-- tocstop -->

## Manually

Make shure CHANGELOG is updated:

- [keep a changelog](https://keepachangelog.com/en/1.0.0/)

Make a git tag for the release:

- [2.6 Git Basics - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

Change `Cargo.toml` with the new version number.

At staging branch, create a version tag:

TODO: integrate with yq

```sh
git switch staging
git tag v$(yq -oy '.package.version' Cargo.toml)
git push origin v$(yq -oy '.package.version' Cargo.toml)
```

At master branch merge the tag:

```sh
git switch master
git merge staging_branch tag_name
git push origin master
```

At the main repository, at the `master` branch:

Before PR, performe a local publish test:

```sh
cargo publish --dry-run
```

```sh
cargo publish
```

## Automatically (CI/CD)

Example with github actions:

```yaml
name: Publish to Crates.io

on:
  push:
    tags:
      - 'v*'  # This triggers the workflow on version tags (e.g., v1.0.0)
    branches:
      - master

jobs:
  publish:
    name: Publish Crate
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Rust
        uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
          profile: minimal
          override: true

      - name: Cache cargo registry
        uses: actions/cache@v2
        with:
          path: |
            ~/.cargo/registry
            ~/.cargo/git
          key: ${{ runner.os }}-cargo-${{ hashFiles('**/Cargo.lock') }}
          restore-keys: ${{ runner.os }}-cargo-

      - name: Install dependencies
        run: cargo build --release

      - name: Publish to crates.io
        env:
          CARGO_REGISTRY_TOKEN: ${{ secrets.CARGO_REGISTRY_TOKEN }}
        run: cargo publish --token $CARGO_REGISTRY_TOKEN
```

- ![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/cwnt-io/candid-gen/rust.yml)
  - check if it is working with the correct yaml
