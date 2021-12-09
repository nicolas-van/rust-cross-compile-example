# rust-cross-compile-example

[![Rust](https://github.com/nicolas-van/rust-cross-compile-example/actions/workflows/rust.yml/badge.svg)](https://github.com/nicolas-van/rust-cross-compile-example/actions/workflows/rust.yml)

A working example of multi targets compilation for Rust using Github Actions.

It compiles a hello world example in Rust using Github Actions to the following architectures:

* Windows x86_64
* MacOSX x86_64
* Linux x86_64, both GNU and Musl libc
* Linux ARMV6 (for Raspberry Pi 1), both GNU and Musl libc
* Linux ARMV7 (for Raspberry Pi 2 and up), both GNU and Musl libc
* Linux ARM64 (mostly for cheaper servers like AWS EC2 t4g line), both GNU and Musl libc

Windows and MacOSX do not actually use cross-compilation and just launch jobs on Windows and MacOSX runners respectively as this is way less painful than trying to compile from Linux. All Linux targets are created from x86_64 Ubuntu runners using true cross-compilation and without relying on Docker. Builds are run in parallel.

See the [workflow configuration file](./.github/workflows/rust.yml).

You can check that the binaries the workflow produces are valid in the [release page](https://github.com/nicolas-van/rust-cross-compile-example/releases) or you can fork this repository. In that case the workflow should run automatically and you will get the same result.
