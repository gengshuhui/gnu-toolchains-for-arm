# Arm GNU Toolchain

## Overview

The GNU Toolchain for the Arm Architecture releases produced by Arm (referred to as **Arm GNU Toolchain**) enable partners, developers, and the community to use new features from recent Arm Architecture and from open-source projects GCC, Binutils, glibc, Newlib, and GDB.

> **Note:** Arm GNU Toolchain releases previously published on the [Arm Developer downloads page](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) are now hosted in this space.

## Features

- Contains integrated and validated packages.
- Supports C and C++ languages.
- Supports CPUs based on the A, R, and M profiles of the Arm architecture (including Cortex-A, Cortex-R, Cortex-M, and Neoverse processors).
- Provides cross-toolchains for Microsoft Windows (x86), Linux (x86_64 and AArch64), and macOS (x86_64) host operating systems.
- Provides different variants of the toolchain which can be used for bare-metal embedded development and for Linux kernel and application development.
- Released twice a year.
- Free to download and use.

## Quality Policy

Arm GNU Toolchain releases are tested using the respective test suites of the source projects to ensure there are no new regressions that affect the quality. However, these releases are:

- Published with no warranty.
- Not necessarily suitable for specific use-cases.
- Community supported.

## Support Policy

Arm GNU Toolchain releases aim to provide easy access to the latest features on a best-effort basis. We do not guarantee that all questions will be answered promptly on public community forums nor that reported issues will be fixed in future releases.

Read the **Get Help** section to find out the best way to get community support. If you wish to make any contributions, those should be made directly to the open-source projects following their respective processes.

> **Note:** GNU Toolchain releases from Arm were previously published as two separate releases:
>
> - [GNU Toolchain for A-profile processors](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-a/downloads)
> - [GNU Arm Embedded Toolchain (R-profile and M-profile)](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)
>
> Arm GNU Toolchain releases unify these two into a single release, and the previous release model has therefore been discontinued. However, the previous releases will continue to be available for reference.

## Contributions

All contributions from Arm are made to the trunk and/or the release branches of the relevant projects.

| Project | Source Code Repository |
|----------|------------------------|
| GNU C/C++ Compiler (GCC)\* | `git://gcc.gnu.org/git/gcc.git` |
| Binutils | `git://sourceware.org/git/binutils-gdb.git` |
| GDB | `git://sourceware.org/git/binutils-gdb.git` |
| Newlib | `git://sourceware.org/git/newlib-cygwin.git` |
| Glibc | `git://sourceware.org/git/glibc.git` |

\* **Note:** GCC sources are picked from an Arm vendor branch which is based on an official GCC release branch. Sometimes, patches are cherry-picked as needed to the Arm vendor branch for binary releases.

