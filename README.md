# `rust-musl-builder`: Build rust for AWS Lambda

Build locally for AWS Lambda machines.
- Includes Protobuf
- From https://github.com/emk/rust-musl-builder

## Build & Build

```sh
time docker build . -t rust-builder
alias rust-builder='docker run -it -v target:/home/rust/src/target  -v cargo-registry:/home/rust/.cargo/registry  -v cargo-git:/home/rust/.cargo/git -v "$(pwd)":/home/rust/src rust-builder'
rust-builder cargo build --release --bin bootstrap
```

- things are in `target/x86_64-unknown-linux-musl/release`

## Caching builds

You may be able to speed up build performance by adding the following `-v` commands to the `rust-musl-builder` alias:

```txt
-v cargo-git:/home/rust/.cargo/git
-v cargo-registry:/home/rust/.cargo/registry
-v target:/home/rust/src/target
```

You will also need to fix the permissions on the mounted volumes:

```sh
rust-musl-builder sudo chown -R rust:rust \
  /home/rust/.cargo/git /home/rust/.cargo/registry /home/rust/src/target
```
