

# GNU Toolchain Release 11.2-2022.02

[Arm GNU Toolchain](https://developer.arm.com/Tools%20and%20Software/GNU%20Toolchain) is a community supported pre-built GNU compiler toolchain for Arm based CPUs.

Arm GNU Toolchain releases consists of cross toolchains for the following host operating systems:

**GNU/Linux**
- Available for x86_64 and AArch64 host architectures
- Available for bare-metal and Linux targets

**Windows**
- Available for x86 host architecture only (compatible with x86_64)
- Available for bare-metal and Linux targets

**macOS**
- Available for Apple silicon host architectures
- Available for x86_64 host architectures for releases up to 14.2.rel1
- Available for bare-metal targets only

Some releases are for specific toolchain variants and might not provide all the toolchain variants.

Please download the correct toolchain variant that suits your development needs.

If you need to access the previous releases of Arm GNU Toolchain, please refer to:
https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads

## Platforms
- [Windows](#windows)
- [Linux](#linux)
- [macOS](#macos)

## What's new in 11.2-2022.02
This release is based on GCC 11.2-2022.02



<h2 id="windows">Windows hosted cross toolchains</h2>

<details>
<summary><strong>1. Windows (mingw-w64-i686) hosted cross toolchains </strong></summary>

| Toolchain | .asc | .sha256asc |
|---|---|---|
| [gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.exe](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.exe) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.exe.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.exe.sha256asc) |
| [gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.zip](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.zip) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.zip.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.zip.sha256asc) |
| [gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.exe](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.exe) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.exe.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.exe.sha256asc) |
| [gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.zip](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.zip) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.zip.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.zip.sha256asc) |
| [gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.exe](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.exe) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.exe.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.exe.sha256asc) |
| [gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.zip](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.zip) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.zip.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.zip.sha256asc) |
| [gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.exe](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.exe) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.exe.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.exe.sha256asc) |
| [gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.zip](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.zip) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.zip.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.zip.sha256asc) |

</details>

---

<h2 id="linux">Linux hosted cross toolchains</h2>

<details>
<summary><strong>2. x86_64 Linux hosted cross toolchains </strong></summary>

| Toolchain | .asc | .sha256asc |
|---|---|---|
| [gcc-arm-11.2-2022.02-x86_64-aarch64-none-elf.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64-none-elf.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64-none-elf.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64-none-elf.tar.xz.sha256asc) |
| [gcc-arm-11.2-2022.02-x86_64-aarch64-none-linux-gnu.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64-none-linux-gnu.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64-none-linux-gnu.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64-none-linux-gnu.tar.xz.sha256asc) |
| [gcc-arm-11.2-2022.02-x86_64-aarch64_be-none-linux-gnu.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64_be-none-linux-gnu.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64_be-none-linux-gnu.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-aarch64_be-none-linux-gnu.tar.xz.sha256asc) |
| [gcc-arm-11.2-2022.02-x86_64-arm-none-eabi.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-arm-none-eabi.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-arm-none-eabi.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-arm-none-eabi.tar.xz.sha256asc) |
| [gcc-arm-11.2-2022.02-x86_64-arm-none-linux-gnueabihf.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-arm-none-linux-gnueabihf.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-arm-none-linux-gnueabihf.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-x86_64-arm-none-linux-gnueabihf.tar.xz.sha256asc) |

</details>

<details>
<summary><strong>3. aarch64 Linux hosted cross toolchains</strong></summary>

| Toolchain | .asc | .sha256asc |
|---|---|---|
| [gcc-arm-11.2-2022.02-aarch64-aarch64-none-elf.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-aarch64-none-elf.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-aarch64-none-elf.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-aarch64-none-elf.tar.xz.sha256asc) |
| [gcc-arm-11.2-2022.02-aarch64-arm-none-eabi.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-arm-none-eabi.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-arm-none-eabi.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-arm-none-eabi.tar.xz.sha256asc) |
| [gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf.tar.xz.sha256asc) |

</details>

---

<h2 id="macos">macOS hosted cross toolchains</h2>

<details>
<summary><strong>4. macOS (x86_64) hosted cross toolchains</strong></summary>

| Toolchain | .asc | .sha256asc |
|---|---|---|
| [gcc-arm-11.2-2022.02-darwin-x86_64-aarch64-none-elf.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-darwin-x86_64-aarch64-none-elf.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-darwin-x86_64-aarch64-none-elf.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-darwin-x86_64-aarch64-none-elf.tar.xz.sha256asc) |
| [gcc-arm-11.2-2022.02-darwin-x86_64-arm-none-eabi.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-darwin-x86_64-arm-none-eabi.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-darwin-x86_64-arm-none-eabi.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-11.2-2022.02-darwin-x86_64-arm-none-eabi.tar.xz.sha256asc) |

</details>

---


<h2 id="source">Source release</h2>

<details>
<summary><strong> Source release artifacts</strong></summary>

| Toolchain | .asc | .sha256asc |
|---|---|---|
| [gcc-arm-src-snapshot-11.2-2022.02.tar.xz](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-src-snapshot-11.2-2022.02.tar.xz) | [.asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-src-snapshot-11.2-2022.02.tar.xz.asc) | [.sha256asc](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-src-snapshot-11.2-2022.02.tar.xz.sha256asc) |



[gcc-arm-src-snapshot-11.2-2022.02-manifest.txt](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-src-snapshot-11.2-2022.02-manifest.txt)

</details>

---

<h2 id="linaro">Linaro ABE example manifests</h2>

<details>
<summary><strong>Linaro ABE example manifest files for x86_64 Linux hosted cross toolchains</strong></summary>

- [gcc-arm-arm-none-eabi-abe-manifest.txt](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-arm-none-eabi-abe-manifest.txt)
- [gcc-arm-arm-none-linux-gnueabihf-abe-manifest.txt](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-arm-none-linux-gnueabihf-abe-manifest.txt)
- [gcc-arm-aarch64-none-elf-abe-manifest.txt](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-aarch64-none-elf-abe-manifest.txt)
- [gcc-arm-aarch64-none-linux-gnu-abe-manifest.txt](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-aarch64-none-linux-gnu-abe-manifest.txt)
- [gcc-arm-aarch64_be-none-linux-gnu-abe-manifest.txt](https://gitlab.arm.com/api/v4/projects/tooling%2Fgnu-toolchains-for-arm/packages/generic/gnu-toolchain/11.2-2022.02/gcc-arm-aarch64_be-none-linux-gnu-abe-manifest.txt)

</details>

---
