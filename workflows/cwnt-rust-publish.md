# cwnt rust release process

> Workflow to publish a Rust package at crates.io
> [The Cargo Book > Publishing on crates.io](https://doc.rust-lang.org/cargo/reference/publishing.html)

<!-- toc -->

## Manually

Make shure CHANGELOG is updated:

- [keep a changelog](https://keepachangelog.com/en/1.0.0/) 

Make a git tag for the release:

- [2.6 Git Basics - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging) 

Before PR, performe a local publish test:

```sh
cargo publish --dry-run
```

```sh
cargo publish
```
