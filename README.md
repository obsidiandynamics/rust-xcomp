`rust-xcomp`
===
[![Docker](https://img.shields.io/docker/pulls/obsidiandynamics/rust-xcomp.svg?style=flat-square)](https://hub.docker.com/r/obsidiandynamics/rust-xcomp)

Cross-compilation support for Rust.

Native linkers are courtesy of [MinGW-w64](https://www.mingw-w64.org/) and [OSXCross](https://github.com/tpoechtrager/osxcross) – supporting `i686` and `x86_64` Windows targets, and Darwin/macOS targets for `x86_64` and `aarch64`/`arm64`.

To compile, run `cargo build --target <target>`, setting `<target>` as needed.