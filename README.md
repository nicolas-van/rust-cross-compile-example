# rust-cross-compile-example

A working example of multi targets compilation for Rust using Github Actions.

It compiles a hello world example in RUST using Github Actions to the following architectures:

* Windows x86_64
* MacOSX x86_64
* Linux x86_64, both GNU and Musl libc
* Linux ARMV6 (for Raspberry Pi 1), both GNU and Musl libc
* Linux ARMV7 (for Raspberry Pi 2 and up), both GNU and Musl libc
* Linux ARM64 (mostly for cheaper servers like AWS EC2 t4g line), both GNU and Musl libc

See the [workflow configuration file](./.github/workflows/rust.yml).

You can also check that the binaries the workflow produces are valid in the [release page](https://github.com/nicolas-van/rust-cross-compile-example/releases).