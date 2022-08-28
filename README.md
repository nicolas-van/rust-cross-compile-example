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

## Known issues:

* All linux GNU libc builds should have an issue with the libc version due to the usage of Debian's current GNU libc version. This is a very well known and documented issue on all Linux systems. It means produced executable will be bound to the current libc version and will be unable to run on older distributions that have an older libc version. Potential solutions:
  * Willingly use an older version of Ubuntu to perform the compilation. (As example Ubuntu 18.) That's clearly not a very sustainable solution but it has the advantage of being very easy to do. (Just changing the version of Ubuntu in the workflow file do the trick.)
  * Use advanced cross-compilation solution like [crosstool-NG](https://crosstool-ng.github.io/) or [dockcross](https://github.com/dockcross/dockcross) (crosstool-NG in docker containers). This is harder to use but it is quite probably the best solution overall.
* Musl libc builds could probably be improved by embedding the Musl libc inside the executable (I don't think it's currently the case).

If you have any solution for these problems feel free to fork the project, modify it in your branch, test the results and then make a pull request. As long as you bring a working enhancement to the project it is unlikely that I refuse a pull request.
