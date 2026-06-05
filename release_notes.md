# __Release Notes__ - Arm GNU Toolchain 14.3.Rel1

## Table of Contents
  - Introduction
  - Changes since __Arm GNU Toolchain 14.2.Rel1__
  - Known Limitations, Issues and Updates
  - Ask Questions
  - Report Bugs
  - Host Support
  - Included Toolchains
  - Released Files
  - Source Code
  - Installation Instructions
    - Verifying the downloaded packages
    - Installing on Linux
    - Installing on macOS
    - Installing on Windows
    - Known Dependencies
  - Invoking GCC
    - Architecture Options
      - -mcpu
      - -mfloat-abi
      - -mthumb
      - Examples
    - Available multilibs
    - C Libraries
      - Additional newlib-nano libraries usage
      - Semihosting
      - Linker scripts & startup code
  - Samples
  - GDB Server for CMSIS-DAP based hardware debugger
  - Building the toolchain from sources using gnu-devtools-for-arm

## Introduction

This is release 14.3.Rel1 of Arm GNU Toolchain.

__Arm GNU Toolchain__ releases package pre-built binaries of GNU Toolchain for various Arm targets. These are community supported and come with no warranty. For more information, please visit the [arm Developer page](https://developer.arm.com/Tools%20and%20Software/GNU%20Toolchain).

This release includes bare-metal and Linux toolchains for various hosts, as described in the Host Support section.


## Changes since __Arm GNU Toolchain 14.2.Rel1__

- Updated GCC to source code based on version 14.3.
- Updated Binutils to source code based on version 2.44.
- Updated GDB to source code based on version 15.
- Updated Glibc to source code based on version 2.40
- Updated Newlib to source code based on trunk.
- Updated Libexpat to source code based om version 2.7.1


## Known Limitations, Issues and Updates

- PR 110796 (https://gcc.gnu.org/bugzilla/show_bug.cgi?id=110796): The Arm architecture provides two instructions for comparing floating-point values.  VCMPE will cause the IEEE floating-point exception status to be updated if the comparison is not well defined while VCMP will leave the exception status unchanged.  The compiler might sometimes choose the wrong instruction for the intended comparison.  Most Arm implementations do not implement hardware trapping of floating-point exceptions so this issue will only matter when both these conditions are met:
    -   A comparison involving NaNs or infinities is performed
    -   The exception status bits are then checked by software

- Release 14.2.Rel1 introduced the Tail Predication codegen feature for our MVE enabled targets to make use of the Tail-Predicated Low Overhead Loop architecture feature. This feature has been backported to our arm-14 vendor branch to offer early access to our users. This feature is in Beta state and can be disabled using the '-mno-dlstp' command-line option. This holds for Release 14.3.Rel1 as well.

- Release 14.3.Rel1 contains backported patches to fix the performance regression reported in PR 116444 https://gcc.gnu.org/bugzilla/show_bug.cgi?id=116444

- As of Release 14.3.Rel1, all toolchains (Linux, Windows, and macOS) now include two GDB executables. GDB with Python scripting support was newly added for Windows and macOS in this release.

    -   GDB with Python scripting support, identified by the "-py" suffix.
        Details for Python-enabled GDB builds:
        -   Windows: built with Python 3.8.10
        -   macOS: built with Python 3.9.7
        -   Linux: built with Python 3.8.20
    -   GDB without Python support, which does not include the "-py" suffix.

    Note: In releases before 13.3.Rel1, Linux toolchains included only a single GDB executable (without the -py suffix), which had Python support by default.
    Refer to the Installation Instructions for steps on installing Python to enable GDB scripting support where applicable.

- Doing IPA on CMSE generates a linker error: The linker will error out when resulting object file contains a symbol for the clone function with the __acle_se prefix that has a non-local binding. Issue occurs when compiling binaries for M-profile Secure Extensions where the compiler may decide to clone a function with the cmse_nonsecure_entry attribute. Although cloning nonsecure entry functions is legal, as long as the clone is only used inside the secure application, the clone function itself should not be seen as a secure entry point and so it should not have the __acle_se prefix. A possible workaround for this is to add a 'noclone' attribute to functions with the 'cmse_nonsecure_entry'. This will prevent GCC from cloning such functions.

- GCC can hang or crash if the input source code uses MVE Intrinsics polymorphic variants in a nested form. The depth of nesting that triggers this issue might vary depending on the host machine. This behaviour is observed when nesting 7 times or more on a high-end workstation. On less powerful machines, this behaviour might be observed with fewer levels of nesting. This issue is reported in https://gcc.gnu.org/bugzilla/show_bug.cgi?id=91937

- PR 32506 (https://sourceware.org/bugzilla/show_bug.cgi?id=32506): when the linker option --gc-sections is used to eliminate unused functions or data it is often the case that the related debug data cannot be removed.  The linker handles this by mapping the information relating to the eliminated data to address zero (or just above that for larger objects).  When a debugger is used to examine programs with real code or data at low addresses this extraneous debug information may cause the debugger to display incorrect symbols or code.  The easiest work-around for this issue is to avoid using --gc-sections when debugging is needed.

- GLIBC 2.39 has dropped support for the libcrypt library. Therefore, the libcrypt library might not be available from a future release of the Arm GNU Toolchain that uses GLIBC 2.39 or later. Users who require libcrypt support are encouraged to look into alternative sources such as libxcrypt.

- Starting with version 14.2.Rel1, RHEL7,  and any earlier versions are no longer supported.
Starting with version 14.3.Rel1, Ubuntu 18.04 and any earlier versions are no longer supported.
Toolchains built on RHEL8 may introduce dependencies—such as libzstd—that are not readily available on RHEL7.
Toolchains built on Ubuntu 20.04 may introduce dependencies that are not readily available on earlier versions of Ubuntu.

- x86_64 Linux cross toolchains are built on RHEL8, using GCC9

- aarch64 Linux toolchains are built on Ubuntu20, using GCC9

- The security issue described in [CVE-2024-0151](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2024-0151) has been fixed. For more information, see the [Cortex-M Security Extensions (CMSE) Security Bulletin](https://developer.arm.com/Arm%20Security%20Center/Cortex-M%20Security%20Extensions).

- From the 14.3.Rel1 release, macOS hosted toolchains for x86_64 architecture is not supported

- The top directory structure from the Windows zip packages has been removed. This means the contents of the package can now be directly extracted. The manifest file in the packages is renamed to manifest.txt

-   Release 14.2.Rel1 introduces support for Windows toolchains with 64-bit executables (mingw-w64-x86_64). These are in addition to the Windows toolchains with 32-bit executables (mingw-w64-i686). Note that if you install a toolchain based on mingw-w64-x86_64, and install the same target toolchain based on mingw-w64-i686, to the same location, then the installed files will overwrite each other.

-   To improve performance on high-end AArch64 processors, when generating AArch64 code, the default generic tuning enforces 32-byte function alignment, and all pre-compiled runtime libraries have been built with this. This might cause an increase in code-size of AArch64 binaries that statically link against these libraries.

## Ask Questions

For any questions, please use the [Arm Community forums](https://community.arm.com/support-forums/f/compilers-and-libraries-forum)


## Report Bugs

Please report any bugs via the [Linaro Bugzilla under "GNU Binary Toolchain" product](https://bugs.linaro.org/enter_bug.cgi?product=GNU%20Binary%20Toolchain).


## Host Support
| Host | Host Identifier<br>(package name) | Toolchain Target |
| -------- | --------------- | ---------------- |
| __Windows on IA-32 or x86_64__ <br><br>*Windows 10 or later* | mingw-w64-i686 | AArch64 Bare-metal<br>AArch64 Linux<br>AArch32 Bare-metal<br>AArch32  Linux hard-float|
| __Windows on x86_64__ <br><br>*Windows 10 or later* | mingw-w64-x86_64 | AArch64 Bare-metal<br>AArch64 Linux<br>AArch32 Bare-metal<br>AArch32  Linux hard-float|
| __Linux on AArch64__<br><br>*These toolchains are built on<br> Ubuntu 20.04 on <br>AArch64, and will likely also <br>be useable on OS versions:<br><br>- later than Ubuntu 20.04<br>* | aarch64 | AArch64 Bare-metal<br>AArch64 Linux<br>AArch32 Bare-metal<br>AArch32 Linux hard-float|
| __Linux on x86_64__<br><br>*These toolchains are built on<br> RHEL8 on x86_64, and<br> will likely also be useable on<br> OS versions:<br><br>- Later than RHEL8<br>- Ubuntu 20.04 or later* | x86_64 |AArch64 Bare-metal<br>AArch64  Linux<br>AArch64 Linux big-endian<br>AArch32 Bare-metal<br>AArch32 Linux hard-float|
| __macOS on Apple silicon__<br><br>*macOS 11 or later* | darwin-arm64 |AArch64 Bare-metal<br>AArch32 Bare-metal|


## Included Toolchains
  The packages of the released GNU toolchain binaries have the following naming convention:

&nbsp;&nbsp;&nbsp;```arm-gnu-toolchain-<Release Version>-<Host>-<Target Triple>.tar.xz```

- In the following table, ```<Target Triple>``` is listed in parentheses in the second column as part of target description.
- The format of `<Release Version>` is:

&nbsp;&nbsp;&nbsp;`<GCC Major Version>.<GCC Minor Version>.[<Feature>-]{Alp|Bet|Rel}<Revision>`
- For Windows, the binaries are provided in zip files and with installers.
- For Linux, the binaries are provided as tarball files.
- For macOS, the binaries are provided as tarball files and pkg files.

<br>

| Toolchain Package Name | Host OS / Target Description |
| --- | ----- |
|arm-gnu-toolchain-14.3.rel1-aarch64-aarch64-none-elf.tar.xz| Host: Linux on AArch64<br> Target: AArch64  bare-metal <br>(aarch64-none-elf)|
|arm-gnu-toolchain-14.3.rel1-aarch64-arm-none-eabi.tar.xz| Host: Linux on AArch64<br> Target: Arch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-14.3.rel1-aarch64-arm-none-linux-gnueabihf.tar.xz|Host: Linux on AArch64<br>Target: AArch32 GNU/Linux target with hard float.<br>(arm-none-linux-gnueabihf)|
|arm-gnu-toolchain-14.3.rel1-aarch64-aarch64-none-linux-gnu.tar.xz|Host: Linux on AArch64<br>Target: AArch64 GNU/Linux<br>(aarch64-none-linux-gnu)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-arm-none-eabi.zip|Host: Windows<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-arm-none-eabi.exe|Host: Windows<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-aarch64-none-elf.zip|Host: Windows<br>Target: AArch64 bare-metal<br> (aarch64-none-elf)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-aarch64-none-elf.exe|Host: Windows<br>Target: AArch64 bare-metal<br> (aarch64-none-elf)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-arm-none-linux-gnueabihf.zip|Host: Windows<br>Target: AArch32 GNU/Linux with hard float<br>(arm-none-linux-gnueabihf)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-arm-none-linux-gnueabihf.exe|Host: Windows<br>Target: AArch32 GNU/Linux with hard float<br>(arm-none-linux-gnueabihf)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-aarch64-none-linux-gnu.zip|Host: Windows<br>Target: AArch64 GNU/Linux<br>(aarch64-none-linux-gnu)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-aarch64-none-linux-gnu.exe|Host: Windows<br>Target: AArch64 GNU/Linux<br>(aarch64-none-linux-gnu)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-x86_64-arm-none-eabi.zip|Host: Windows<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-x86_64-arm-none-eabi.exe|Host: Windows<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-x86_64-aarch64-none-elf.zip|Host: Windows<br>Target: AArch64 bare-metal<br> (aarch64-none-elf)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-x86_64-aarch64-none-elf.exe|Host: Windows<br>Target: AArch64 bare-metal<br> (aarch64-none-elf)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-x86_64-arm-none-linux-gnueabihf.zip|Host: Windows<br>Target: AArch32 GNU/Linux with hard float<br>(arm-none-linux-gnueabihf)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-x86_64-arm-none-linux-gnueabihf.exe|Host: Windows<br>Target: AArch32 GNU/Linux with hard float<br>(arm-none-linux-gnueabihf)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-x86_64-aarch64-none-linux-gnu.zip|Host: Windows<br>Target: AArch64 GNU/Linux<br>(aarch64-none-linux-gnu)|
|arm-gnu-toolchain-14.3.rel1-mingw-w64-x86_64-aarch64-none-linux-gnu.exe|Host: Windows<br>Target: AArch64 GNU/Linux<br>(aarch64-none-linux-gnu)|
|arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-elf.tar.xz|Host: Linux on x86_64<br>Target: AArch64  bare-metal<br>triple: aarch64-none-elf|
|arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-linux-gnu.tar.xz|Host: Linux on x86_64<br>Target: AArch64 GNU/Linux<br>(aarch64-none-linux-gnu)|
|arm-gnu-toolchain-14.3.rel1-x86_64-aarch64_be-none-linux-gnu.tar.xz|Host: Linux on x86_64<br>Target: AArch64 GNU/Linux big-endian<br>(aarch64_be-none-linux-gnu)|
|arm-gnu-toolchain-14.3.rel1-x86_64-arm-none-eabi.tar.xz|Host: Linux on x86_64<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-14.3.rel1-x86_64-arm-none-linux-gnueabihf.tar.xz|Host: Linux on x86_64<br>Target: AArch32 GNU/Linux  with hard float<br>(arm-none-linux-gnueabihf)|
|arm-gnu-toolchain-14.3.rel1-darwin-arm64-aarch64-none-elf.tar.xz|Host: macOS on Apple silicon<br>Target: AArch64 bare-metal<br>triple: aarch64-none-elf<br> (aarch64-none-elf)|
|arm-gnu-toolchain-14.3.rel1-darwin-arm64-aarch64-none-elf.pkg|Host: macOS on Apple silicon<br>Target: AArch64 bare-metal<br>triple: aarch64-none-elf<br> (aarch64-none-elf)|
|arm-gnu-toolchain-14.3.rel1-darwin-arm64-arm-none-eabi.tar.xz|Host: macOS on Apple silicon<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-14.3.rel1-darwin-arm64-arm-none-eabi.pkg|Host: macOS on Apple silicon<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|


## Released Files
|File Name|Description|
|---|---|
|```arm-gnu-toolchain-*.tar.xz```|Toolchain binaries|
|```arm-gnu-toolchain-*.zip```|	Zipped toolchain binaries for Windows|
|```arm-gnu-toolchain-*.exe```|Toolchain installer for Windows|
|```arm-gnu-toolchain-*.pkg```|Toolchain installer for macOS|
|```arm-gnu-toolchain-*-src-snapshot-*.tar.xz```|Toolchain sources|
|```arm-gnu-toolchain-*-src-manifest.txt```| List of remote repositories and the revisions<br>of the source code used for building the toolchain|
|```*.asc```|MD5 checksum files for sources and binaries|
|```*.sha256asc```|SHA256 checksum files for sources and binaries|


## Source Code

The sources for this release are provided in the source tar ball, arm-gnu-toolchain-src-snapshot-14.3.rel1.tar.xz, and includes the following items:

|Project|Version&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Repository/Branch/Revision|
|-------|-------|-----------------|
| GCC |  *based on* 14.3 | git://gcc.gnu.org/git/gcc.git<br>branch: ARM/arm-14.3<br>revision: c6ee55bf5766d1d38e57d92e3a757fde4722d55d  <br>For information on vendor branches, see https://gcc.gnu.org/gitwrite.html#vendor |
| glibc | 2.40  |git://sourceware.org/git/glibc.git<br>branch: release/2.40/master<br>revision: c8e10f14328518954072df64aafd574e67cfdde5 |
| newlib<br>newlib-nano |  | git://sourceware.org/git/newlib-cygwin.git<br>revision: 2f43c4b625a1f72dc794144c799bfa4d9e812716 |
| binutils | *based on* 2.44 | git://sourceware.org/git/binutils-gdb.git<br>branch: users/ARM/binutils-2_44-branch<br>revision: 7f90426069ff1eaab17fea8dbb2f4d558cba33f4 |
| GDB |*based on* 15 | git://sourceware.org/git/binutils-gdb.git<br>branch: gdb-15-branch<br>revision: 123beb129ec937952844e9c867c9c0333123b95f |
| libexpat |*based on* 2.7.1 | Sources are provided in release source tar ball |
| Linux Kernel || git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git<br>revision: v4.20.13 |
| libgmp |*based on* 6.2 | Sources are provided in release source tar ball |
| libisl |*based on* 0.15| Sources are provided in release source tar ball |
| libmpfr |*based on* 3.1.6| Sources are provided in release source tar ball |
| libmpc |*based on* 1.0.3| Sources are provided in release source tar ball |
| libiconv |*based on* 1.15 | Sources are provided in release source tar ball |


## Installation Instructions

### Verifying the downloaded packages

You may check using MD5 checksum as follows:

```
$ md5sum --check arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-linux-gnu.tar.xz.asc
arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-linux-gnu.tar.xz: OK
```

Similarly for using SHA256 checksum, use the following instructions:

```
$ sha256sum --check arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-linux-gnu.tar.xz.sha256asc
arm-gnu-toolchain-14.3.rel1-x86_64-aarch64-none-linux-gnu.tar.xz: OK
```

### Installing on Linux

To install a toolchain on Linux, unpack the tarball to the preferred installation directory using the following instruction:

**On x86_64:**

    $ tar xJf arm-gnu-toolchain-14.3.rel1-x86_64-<TRIPLE>.tar.xz -C /path/to/install/dir

**On aarch64:**

    $ tar xJf arm-gnu-toolchain-14.3.rel1-aarch64-<TRIPLE>.tar.xz -C /path/to/install/dir

GDB can be used with Python support or without Python support. To use GDB with Python support, Python 3.8 is required to be installed, and on Ubuntu 20.04 or later you might also need to install libncurses5 or libncursesw5. You might need to install Python 3.8 from source. The information about installing Python can be found from other sources or websites, unaffiliated to Arm, for example, from [docs.python.org](https://docs.python.org/3.11/using/unix.html#building-python), or from [LinuxCapable](https://www.linuxcapable.com/install-python-3-8-on-ubuntu-linux/). For GDB to be able to detect the existence of an installed Python 3.8 library on the system, you might also need to set the `PYTHONPATH` and `PYTHONHOME` environment variables. Set `PYTHONHOME` to the location where the Python 3.8 libraries are. For example, if Python 3.8 was installed to `/usr/lib` or `/usr/lib64`, then set `PYTHONHOME=/usr`. In order to find the correct value for `PYTHONPATH`, run  `python3.8 -c "import sys; print(sys.path)"` and look for the path ending in `/python3.8`. Set `PYTHONPATH=<that path ending in /python3.8>`.

### Installing on macOS

To install a toolchain on macOS, unpack the tarball to the preferred installation directory using the following instruction:

**On darwin-arm64:**

    $ tar xJf arm-gnu-toolchain-14.3.rel1-darwin-arm64-<TRIPLE>.tar.xz -C /path/to/install/dir


### Installing on Windows

To install the toolchain on Windows, you may choose to run the installer:

    arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-<TRIPLE>.exe

and follow the instructions. The installer can also be run on the command line. When run on the command-line, the following options can be set:

    - /S Run in silent mode
    - /P Adds the installation bin directory to the system PATH
    - /R Adds an InstallFolder registry entry for the install.

For example, to install the tools silently, amend users PATH and add registry entry:

    > arm-gnu-toolchain-14.3.rel1-mingw-w64-i686-<TRIPLE>.exe /S /P /R

Alternatively, you may use the zip package if you cannot run the installer. In order to do so, you must extract the content of the zip file at a preferred folder.

Arm recommends that you always install into the default installation location. Installing into a different location could expose your system to risks associated with weaker access permissions. For example, the access permissions inherited from the installation directory might allow non-admin users to modify the installed content. Arm recommends restricting write access, to any custom installation location, to only the users who are allowed to run the installer.


### Known Dependencies

- Using GDB with Python support, on Linux hosts, requires installation of Python3.8, Python3.8-dev or libpython3.8.
- aarch64_be-none-linux-gnu-gdb and aarch64_be-none-linux-gnu-gdb-py on Linux hosts requires liblzma.so.5.
- Toolchains dedicated for Windows host require mingw-w64 library, a complete runtime environment for GCC.
- The following executables in the Windows hosted toolchains:
    - aarch64-none-linux-gnu-dwp.exe
    - aarch64-none-linux-gnu-ld.gold.exe
    - arm-none-linux-gnueabihf-dwp
    - arm-none-linux-gnueabihf-ld.gold.exe

  have additional dependencies on the following dlls:
   - libwinpthread-1.dll
   - libgcc_s_sjlj-1.dll
   - libstdc++-6.dll
   - libgcc_s_dw2-1.dll

  You can obtain the required dlls from the MinGW-W64 GCC-8.1.0 packages from SourceForge:

   - i686-posix-sjlj
   - i686-posix-dwarf


## Invoking GCC

On Linux and macOS, either invoke with the complete path like this:

    $ <install-dir>/arm-gnu-toolchain-14.3.rel1-<HOST_ARCH>-aarch64-none-elf/bin/aarch64-none-elf-gcc

where, depending on the host, <HOST_ARCH> is one of:

    x86_64
    aarch64
    darwin-arm64

Or set the path and then invoke the toolchain like this:

    $ export PATH=$PATH:<install-dir>/arm-gnu-toolchain-14.3.rel1-<HOST_ARCH>-aarch64-none-elf/bin
    $ aarch64-none-elf-gcc --version

On Windows, although the above approaches also work, it can be more convenient to either have the installer register environment variables, or run ```<install-dir>\bin\gccvar.bat``` to set environment variables for the current cmd.

For Windows zip package, after extracting the files, we can invoke the toolchain either using the complete path as follows:

    <install-dir>\bin\aarch64-none-elf-gcc

or run ```<install-dir>\bin\gccvar.bat``` to set environment variables for the
current cmd.


### Architecture Options

This toolchain is built and optimized for Arm processors.

This section describes how to invoke GCC/G++ with the correct command-line options for variants of Cortex-A, Cortex-R and Cortex-M processors.

    $ aarch64-none-elf-gcc [-mthumb] -mcpu=CPU[+extension...] -mfloat-abi=ABI

#### -mcpu:

For the permissible CPU names and extensions, see the GCC online manual: https://gcc.gnu.org/onlinedocs/gcc-14.3.0/gcc/ARM-Options.html#index-mcpu-2

Use the optional extension name with -mcpu to disable the extensions that are not present in the CPU of your choice.

By default, -mfpu=auto and this enables the compiler to automatically select the floating-pointing and Advanced SIMD instructions based on the -mcpu option and extension.

#### -mfloat-abi:

If floating-point or Advanced SIMD instructions are present, then use the -mfloat-abi option to control the floating-point ABI, or use -mfloat-abi=soft to disable floating-point and Advanced SIMD instructions.

For the permissible values of -mfloat-abi, see the GCC online manual: https://gcc.gnu.org/onlinedocs/gcc-14.3.0/gcc/ARM-Options.html#index-mfloat-abi

#### -mthumb:

When using processors that can execute in Arm state and Thumb state, use -mthumb to generate code for Thumb state.

#### Examples:

**Examples with no floating-point and Advanced SIMD instructions:**

    $ arm-none-eabi-gcc -mcpu=cortex-m7+nofp
    $ arm-none-eabi-gcc -mcpu=cortex-r5+nofp -mthumb
    $ arm-none-eabi-gcc -mcpu=cortex-a53+nofp -mthumb
    $ arm-none-eabi-gcc -mcpu=cortex-a57 -mfloat-abi=soft -mthumb

**Examples with single-precision floating-point with soft-float ABI:**

    $ arm-none-eabi-gcc -mcpu=cortex-m7+nofp.dp -mfloat-abi=softfp
    $ arm-none-eabi-gcc -mcpu=cortex-r5+nofp.dp -mfloat-abi=softfp -mthumb

**Examples with single-precision floating-point with hard-float ABI:**

    $ arm-none-eabi-gcc -mcpu=cortex-m7+nofp.dp -mfloat-abi=hard
    $ arm-none-eabi-gcc -mcpu=cortex-r5+nofp.dp -mfloat-abi=hard -mthumb

**Examples with double-precision floating-point with soft-float ABI:**

    $ arm-none-eabi-gcc -mcpu=cortex-m7 -mfloat-abi=softfp
    $ arm-none-eabi-gcc -mcpu=cortex-r5 -mfloat-abi=softfp -mthumb

**Examples with double-precision floating-point with hard-float ABI:**

    $ arm-none-eabi-gcc -mcpu=cortex-m7 -mfloat-abi=hard
    $ arm-none-eabi-gcc -mcpu=cortex-r5 -mfloat-abi=hard -mthumb

**Example with floating-point and Advanced SIMD instructions with soft-float ABI:**

    $ arm-none-eabi-gcc -mcpu=cortex-a53 -mfloat-abi=softfp -mthumb

**Example with floating-point and Advanced SIMD instructions with hard-float ABI:**

    $ arm-none-eabi-gcc -mcpu=cortex-a53 -mfloat-abi=hard -mthumb

**Example with MVE and floating-point with soft-float ABI:**

    $ arm-none-eabi-gcc -mcpu=cortex-m55 -mfloat-abi=softfp

**Example with MVE and floating-point with hard-float ABI:**

    $ arm-none-eabi-gcc -mcpu=cortex-m55 -mfloat-abi=hard

### Available multilibs

Arm GNU Toolchain 14.3.Rel1 supports a set of multilibs in each toolchain.

To list all multilibs supported by any of the toolchain, use ```--print-multi-lib``` option. For example,

    $ arm-none-eabi-gcc --print-multi-lib

To check which multilib is selected by the arm-none-eabi toolchain based on -mthumb, -mcpu, -mfpu and -mfloat-abi command line options:

    $ arm-none-eabi-gcc [-mthumb] -mcpu=CPU -mfpu=FPU -mfloat-abi=ABI --print-multi-dir

For example:

    $ arm-none-eabi-gcc -mcpu=cortex-a55 -mfpu=auto -mfloat-abi=hard --print-multi-dir
    thumb/v8-a+simd/hard

    $ arm-none-eabi-gcc -mcpu=cortex-r5 -mfpu=auto -mfloat-abi=softfp --print-multi-dir
    thumb/v7+fp/softfp

    $ arm-none-eabi-gcc -mcpu=cortex-m0 -mfpu=auto -mfloat-abi=soft --print-multi-dir
    thumb/v6-m/nofp

### C Libraries

*This section only applies for arm-none-eabi targets.*

Arm GNU Toolchain 14.3.Rel1 is released with two prebuilt C libraries based on newlib, for arm-none-eabi target.

One is the standard newlib and the other is newlib-nano for reduced code size. To distinguish them, the nano versions are renamed with _nano suffix:

    libc.a --> libc_nano.a
    libg.a --> libg_nano.a

To use newlib-nano, users should provide additional gcc compile and link time option:

    --specs=nano.specs

At compile time, a 'newlib.h' header file especially configured for newlib-nano will be used if --specs=nano.specs is passed to the compiler.

nano.specs also handles two additional gcc libraries: libstdc++_nano.a and libsupc++_nano.a, which are optimized for code size.

For example:

    $ arm-none-eabi-gcc src.c --specs=nano.specs ${OTHER_OPTIONS}

This option can also work together with other specs options such as:

    --specs=rdimon.specs

Please note that --specs=nano.specs is both a compiler and linker option. Be sure to include in both compiler and linker options if compiling and linking are separated.

#### Additional newlib-nano libraries usage

Formatted input/output of floating-point number are implemented as weak symbol. If you want to use %f, you have to pull in the symbol by explicitly specifying "-u" command option.

    -u _scanf_float
    -u _printf_float

e.g. to output a float, the command line is like:

    $ arm-none-eabi-gcc --specs=nano.specs -u _printf_float ${OTHER_LINK_OPTIONS}

#### Semihosting

Users can choose to use or not use semihosting by using the following instructions.

If you need semihosting, link as follows:

    $ arm-none-eabi-gcc --specs=rdimon.specs ${OTHER_LINK_OPTIONS}

If you don't need semihosting or if you use retarget, link as follows:

    $ arm-none-eabi-gcc --specs=nosys.specs ${OTHER_LINK_OPTIONS}

#### Linker scripts & start-up code

This section only applies for arm-none-eabi targets.

Latest update of linker scripts template and start-up code is available on
https://developer.arm.com/tools-and-software/embedded/cmsis


## Samples

*This section only applies for arm-none-eabi targets.*

Examples are available at:

    <install-dir>/share/gcc-arm-none-eabi/samples

Read readme.txt under it for further information.


## GDB Server for CMSIS-DAP based hardware debugger

*This section only applies for arm-none-eabi targets.*

CMSIS-DAP is the interface firmware for a Debug Unit that connects the Debug Port to USB.  More detailed information can be found at http://www.keil.com/support/man/docs/dapdebug/.

A software GDB server is required for GDB to communicate with CMSIS-DAP based hardware debugger.  The pyOCD is an implementation of such GDB server that is written in Python and under Apache License.

For those who are using this toolchain and have a board with CMSIS-DAP based debugger, the pyOCD is our recommended gdb server.  More information can be found at https://github.com/pyocd/pyOCD.


## Building the toolchain from sources using gnu-devtools-for-arm

If you would like to build a toolchain yourself using the source revisions used for this release, you can do so using the scripts in the gnu-devtools-for-arm project.

Note that the scripts in the gnu-devtools-for-arm project are meant to rebuild a toolchain that is similar to the released toolchain. The toolchains built using this method are not identical to the released binaries of Arm GNU Toolchain because the scripts used to build the released toolchains, and scripts in the gnu-devtools-for-arm project, are currently in different repositories and might contain different updates.

The instructions for building the toolchain are provided in the [README.md](https://gitlab.arm.com/tooling/gnu-devtools-for-arm/-/blob/main/README.md) file from the gnu-devtools-for-arm project.

---
