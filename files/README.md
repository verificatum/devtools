# Verificatum Mix-Net Package

## Overview

**This package is solely intended for demonstration purposes** and
contains [VMN](https://github.com/verificatum/verificatum-vmn) and the
distributions of the packages that it needs, including the optional
components which improve its speed, i.e.,
[VCR](https://github.com/verificatum/verificatum-vcr),
[GMPMEE](https://github.com/verificatum/verificatum-gmpmee),
[VMGJ](https://github.com/verificatum/verificatum-vmgj),
[VEC](https://github.com/verificatum/verificatum-vec), and
[VECJ](https://github.com/verificatum/verificatum-vecj).

You accept the [GNU Affero General Public License Version
  3.0](https://www.gnu.org/licenses/agpl-3.0.en.html) by using this
  software. This license should be present in the file `COPYING` in
  this directory. Please read the warnings at the end of this file.

## Requirements

This software aims to be as portable as possible across Unix-flavored
platforms by following the POSIX standard, only using standard tools,
no language extensions, and minimizing the number of dependencies.

#### Build tools

How the necessary tools are installed should not matter, but there are
minor differences and bugs which makes it hard to guarantee on all
platforms. Building requires [GCC](https://gcc.gnu.org) (or
[Clang](https://clang.llvm.org)),
[Make](https://www.gnu.org/software/make),
[Autoconf](https://www.gnu.org/software/autoconf),
[Automake](https://www.gnu.org/software/automake),
[Libtool](https://www.gnu.org/software/libtool), and
[M4](https://www.gnu.org/software/m4), and Java Development Kit, e.g.,
[OpenJDK](https://openjdk.java.net), or drop-in replacements.

#### Dependencies

The native code depends on [GMP](https://gmplib.org) and the software
uses some standard JDK libraries, but it has no other
dependencies. OpenJDK 8 suffices, but it is prudent to install the
most recent JDK.

#### Platform Specific Instructions

We have collected some notes on how to install the necessary libraries
and set up environments on selected platforms at
https://www.verificatum.org.


## Compile and Install

Note that some commands in the `Makefile` are run using `sudo` or
`doas`. Simply run

        make install

which configures, makes, and installs each package in the default
location. Typically this is `/usr/local/bin`, `/usr/local/share/java`,
and `/usr/local/lib`. This also initializes the default random source
to `/dev/urandom`, which may, or may not, be suitable on your
platform.

To delete all files that you installed, you can run

        make uninstall

You can run all tests using

        make check

This takes a long time to complete, so please be patient.

Finally, you can run the demo found in
`verificatum-vmn-<VERSION>/demo/mixnet` by simply using

        make demo

This runs the distributed key generation, generates demo ciphertexts,
mixes the ciphertexts (re-encrypts, permutes, and decrypts), and
finally it runs the reference implementation of the verifier of the
universally verifiable proof.


## Warning!

**This install package is solely intended for demonstration
  purposes. There should probably never be a general purpose
  installation package for security reasons.**

**Do not use this software in any real application if you do not
  understand the functionality and security guarantees that this
  software provides, and does not provide.**

**There are many complex aspects of real-world security (even beyond
  computer security) which are out of scope of this project, e.g.,
  protecting configuration files, protecting against DoS attacks,
  general intrusion protection, procedures for operators, etc. The
  objective of this project is rooted in the Unix philosophy:**

**"Do one thing and do it well."**

**This a feature, since it allows choosing how to provide the needed
  protection in whatever way is most suitable for the application on a
  given platform and in a given setting.**

**Unfortunately, it means that YOU must understand what the
  requirements of your application are and take the necessary steps to
  ensure that they are satisfied.**

**For actual use we therefore STRONGLY suggest that you read the
  `README.md` file, and perhaps the `README_DEV.md` file, of each
  separate package. Install and verify your installation separately
  for each package to make sure that it is installed properly on your
  system.**

**Read all whitepapers and other material at
  https://www.verificatum.org as well to make sure that you understand
  how the software is used.**
