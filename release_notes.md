# __Release Notes__ - Arm GNU Toolchain 12.2.MPACBTI-Bet1

## Table of Contents
  - Introduction
  - Changes since __Arm GNU Toolchain 11.3.Rel1__
  - Known Issues
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
      - -mbranch-protection
    - Available multilibs
    - C Libraries
      - Additional newlib-nano libraries usage
      - Semihosting
      - Non-semihosting/retarget
      - Linker scripts & startup code
  - Samples
  - GDB Server for CMSIS-DAP based hardware debugger
  - Building Toolchain from sources using Linaro's ABE
    - Instructions

## Introduction

This is release __12.2.MPACBTI-Bet1__ of __Arm GNU Toolchain__.
This is a Beta release that supports Cortex-M85 and the Cortex-M PACBTI extension, and therefore this release only includes the arm-none-eabi toolchain triplet.
Toolchains described as Beta have not had the same level of testing as the other toolchains.
This is not a production release and does not replace the previous release of 11.3.Rel1 for production use.


Arm GNU Toolchain releases package pre-built binaries of GNU Toolchain for various Arm targets. These are community supported and come with no warranty. For more information, please visit the [arm Developer page](https://developer.arm.com/Tools%20and%20Software/GNU%20Toolchain).

This release includes bare-metal toolchains for various hosts, as described in the [Host Support](#host-support) section.


## Changes since __Arm GNU Toolchain 11.3.Rel1__

- Updated GCC to source code based on version 12.2, with additional patches to support Cortex-M PACBTI extension.
- Updated Newlib source code to a version on trunk, with additional patches to support Cortex-M PACBTI extension.
- Updated Binutils source code to a version on trunk.
- Updated Glibc to version 2.36.
- Updated GDB source code to a version on trunk.


## Known Issues

1. This release does not support GNU C nested functions when branch protection is enabled using the -mbranch-protection option.

2. The leaf functions in a small subset of Arm assembly (.S) files contain CFI directives that might report incorrect register contents during debug. However, this does not affect exception handling. The affected .S files are in the __newlib/libc/machine/arm__ directory from the Newlib sources.

3. In the Linux hosted toolchains, GDB is provided with Python support. In the Windows and macOS hosted toolchains, GDB is provided without Python support.

4. When you decompress the windows packages, the decompression requests permission to overwrite certain files. This is because the files have similar names with different case, which are treated as identical names on a Windows host. You can choose to overwrite the files with identical names.

5. Doing IPA on CMSE generates a linker error: The linker will error out when resulting object file contains a symbol for the clone function with the __acle_se prefix that has a non-local binding. Issue occurs when compiling binaries for M-profile Secure Extensions where the compiler may decide to clone a function with the cmse_nonsecure_entry attribute. Although cloning nonsecure entry functions is legal, as long as the clone is only used inside the secure application, the clone function itself should not be seen as a secure entry point and so it should not have the __acle_se prefix. A possible workaround for this is to add a 'noclone' attribute to functions with the 'cmse_nonsecure_entry'. This will prevent GCC from cloning such functions.

6. GCC can hang or crash if the input source code uses MVE Intrinsics polymorphic variants in a nested form. The depth of nesting that triggers this issue might vary depending on the host machine. This behaviour is observed when nesting 7 times or more on a high-end workstation. On less powerful machines, this behaviour might be observed with fewer levels of nesting. This issue is reported in https://gcc.gnu.org/bugzilla/show_bug.cgi?id=91937


## Ask Questions

For any questions, please use the [Arm Community forums](https://community.arm.com/developer/tools-software/tools)


## Report Bugs

Please report any bugs via the [Linaro Bugzilla under "GNU Binary Toolchain" product](https://bugs.linaro.org/enter_bug.cgi?product=GNU%20Binary%20Toolchain).


## Host Support
| Host | Host Identifier<br>(package name) | Toolchain Target |
| -------- | --------------- | ---------------- |
| __Windows on IA-32 or x86_64__ <br><br>*Windows 10 or later* | mingw-w64-i686 | AArch32 Bare-metal |
| __Linux on AArch64__<br><br>*These toolchains are built on<br> and for Ubuntu 18.04 on <br>AArch64, and will likely also <br>be useable on OS versions:<br><br>- later than Ubuntu 18.04<br>- RHEL8* | aarch64 | AArch32 Bare-metal |
| __Linux on x86_64__<br><br>*These toolchains are built on<br> and for RHEL7 on x86_64, and<br> will likely also be useable on<br> OS versions:<br><br>- RHEL8<br>- Ubuntu 18.04 or later* | x86_64 | AArch32 Bare-metal |
| __Mac OS X on x86_64__<br><br>*Mac OS X 10.15 or later* | darwin-x86_64 | AArch32 Bare-metal |


## Included Toolchains
  The package names of the released GNU toolchain binaries have the following naming convention:

&nbsp;&nbsp;&nbsp;```arm-gnu-toolchain-<Release Version>-<Host>-<Target Triple>.tar.xz```

- In the following table, ```<Target Triple>``` is listed in parentheses in the second column as part of target description.
- For Windows, the binaries are provided in zip files and with installers.
- For Linux, the binaries are provided as tarball files.
- For Mac OS X, the binaries are provided as tarball files and pkg files.

<br>

| Toolchain Package Name | Host OS / Target Description |
| --- | ----- |
|arm-gnu-toolchain-12.2.mpacbti-bet1-aarch64-arm-none-eabi.tar.xz| Host: AArch64 Linux<br> Target: Arch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-12.2.mpacbti-bet1-mingw-w64-i686-arm-none-eabi.zip|Host: Windows<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-12.2.mpacbti-bet1-mingw-w64-i686-arm-none-eabi.exe|Host: Windows<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-12.2.mpacbti-bet1-x86_64-arm-none-eabi.tar.xz|Host: x86_64 Linux<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-12.2.mpacbti-bet1-darwin-x86_64-arm-none-eabi.tar.xz|Host: x86_64 Darwin<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|
|arm-gnu-toolchain-12.2.mpacbti-bet1-darwin-x86_64-arm-none-eabi.pkg|Host: x86_64 Darwin<br>Target: AArch32 bare-metal<br>(arm-none-eabi)|


## Released Files
|File Name|Description|
|---|---|
|```arm-gnu-toolchain-*.tar.xz```|Toolchain binaries|
|```arm-gnu-toolchain-*.zip```|	Zipped toolchain binaries for Windows|
|```arm-gnu-toolchain-*.exe```|Toolchain installer for Windows|
|```arm-gnu-toolchain-*.pkg```|Toolchain installer for Mac|
|```arm-gnu-toolchain-*-src-snapshot-*.tar.xz```|Toolchain sources|
|```arm-gnu-toolchain-*-src-manifest.txt```| List of remote repositories and the revisions<br>of the source code used for building the toolchain|
|```arm-gnu-toolchain-*-abe-manifest.txt```|Input files for the Linaro ABE build system.|
|```*.asc```|MD5 checksum files for sources and binaries|
|```*.sha256asc```|SHA256 checksum files for sources and binaries|


## Source Code

The sources for this release are provided in the source tar ball, arm-gnu-toolchain-src-snapshot-12.2.mpacbti-bet1.tar.xz, and includes the following items:

|Project|Version&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Repository/Branch/Revision|
|-------|-------|-----------------|
| GCC |  *based on* 12.2 | https://gcc.gnu.org/git/gcc.git<br>branch: vendors/ARM/heads/arm-12-m-pacbti<br>revision: 11d19ae7b3aded18f52b1accfd4ec5051951495b|
| glibc |2.36  |https://sourceware.org/git/glibc.git<br>branch: master-2.36<br>revision: e982657073c4db21459ffd9e17bc505b1d64b876|
| newlib<br>newlib-nano|  | Sources are provided in release source tar ball |
| binutils| *based on* trunk | https://sourceware.org/git/binutils-gdb.git<br>revision: 12f26cb22e56ab8c26dd5a00f32158af561da4cb|
| GDB |*based on* trunk | https://sourceware.org/git/binutils-gdb.git<br>revision: a01567f4f7fbbc6ce1492b359c762fcf39e71b4b|
| libexpat |*based on* 2.2.5 | Sources are provided in release source tar ball |
| Linux Kernel || git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git<br>revision: v4.20.13|
| libgmp |*based on* 6.2 | Sources are provided in release source tar ball |
| libisl |*based on* 0.15| Sources are provided in release source tar ball |
| libmpfr |*based on* 3.1.6| Sources are provided in release source tar ball |
| libmpc |*based on* 1.0.3| Sources are provided in release source tar ball |
| libiconv |*based on* 1.15 | Sources are provided in release source tar ball |


## Installation Instructions

### Verifying the downloaded packages

You may check using MD5 checksum as follows:

```
$ md5sum --check arm-gnu-toolchain-12.2.mpacbti-bet1-x86_64-arm-none-eabi.tar.xz.asc
arm-gnu-toolchain-12.2.mpacbti-bet1-x86_64-arm-none-eabi.tar.xz: OK
```

Similarly for using SHA256 checksum, use the following instructions:

```
$ sha256sum --check arm-gnu-toolchain-12.2.mpacbti-bet1-x86_64-arm-none-eabi.tar.xz.sha256asc
arm-gnu-toolchain-12.2.mpacbti-bet1-x86_64-arm-none-eabi.tar.xz: OK
```

### Installing on Linux

To install a toolchain on Linux, unpack the tarball to the preferred installation directory using the following instruction:

**On x86_64:**

    $ tar xJf arm-gnu-toolchain-12.2.mpacbti-bet1-x86_64-<TRIPLE>.tar.xz -C /path/to/install/dir

**On aarch64:**

    $ tar xJf arm-gnu-toolchain-12.2.mpacbti-bet1-aarch64-<TRIPLE>.tar.xz -C /path/to/install/dir

If you want to use gdb, then Python3.8 is required to be installed.

### Installing on macOS

To install a toolchain on macOS, unpack the tarball to the preferred installation directory using the following instruction:

**On darwin-x86_64:**

    $ tar xJf arm-gnu-toolchain-12.2.mpacbti-bet1-darwin-x86_64-<TRIPLE>.tar.xz -C /path/to/install/dir


### Installing on Windows

To install the toolchain on Windows, you may choose to run the installer:

    arm-gnu-toolchain-12.2.mpacbti-bet1-mingw-w64-i686-<TRIPLE>.exe

and follow the instructions. The installer can also be run on the command line. When run on the command-line, the following options can be set:

    - /S Run in silent mode
    - /P Adds the installation bin directory to the system PATH
    - /R Adds an InstallFolder registry entry for the install.

For example, to install the tools silently, amend users PATH and add registry entry:

    > arm-gnu-toolchain-12.2.mpacbti-bet1-mingw-w64-i686-<TRIPLE>.exe /S /P /R

Alternatively, you may use the zip package if you cannot run the installer. In order to do so, you must extract the content of the zip file at a preferred folder.


### Known Dependencies

- GDB's Python support on Linux hosts requires installation of Python3.8, Python3.8-dev or libpython3.8.
- Toolchains dedicated for Windows host require mingw-w64 library, a complete runtime environment for GCC.


## Invoking GCC

On Linux and macOS, either invoke with the complete path like this:

    $ <install-dir>/arm-gnu-toolchain-12.2.mpacbti-bet1-<HOST_ARCH>-arm-none-eabi/bin/arm-none-eabi-gcc

where, depending on the host, <HOST_ARCH> is one of:

    x86_64
    aarch64
    darwin-x86_64

Or set the path and then invoke the toolchain like this:

    $ export PATH=$PATH:<install-dir>/arm-gnu-toolchain-12.2.mpacbti-bet1-<HOST_ARCH>-arm-none-eabi/bin
    $ arm-none-eabi-gcc --version

On Windows, although the above approaches also work, it can be more convenient to either have the installer register environment variables, or run ```<install-dir>\bin\gccvar.bat``` to set environment variables for the current cmd.

For Windows zip package, after extracting the files, we can invoke the toolchain either using the complete path as follows:

    <install-dir>\bin\arm-none-eabi-gcc

or run ```<install-dir>\bin\gccvar.bat``` to set environment variables for the
current cmd.


### Architecture Options

This toolchain is built and optimized for Arm processors.

This section describes how to invoke GCC/G++ with the correct command-line options for variants of Cortex-A, Cortex-R and Cortex-M processors.

    $ arm-none-eabi-gcc [-mthumb] -mcpu=CPU[+extension...] -mfloat-abi=ABI [-mbranch-protection=PROTECTION]

#### -mcpu:

For the permissible CPU names and extensions, see the GCC online manual: https://gcc.gnu.org/onlinedocs/gcc-12.2.0/gcc/ARM-Options.html#index-mcpu-2

To use Cortex-M85, use -mcpu=cortex-m85.
For Cortex-M85 you can use the following extensions:

    +nopacbti
    +nomve.fp
    +nomve
    +nofp
    +nodsp

To use Pointer Authentication or Branch Target Identification with -march=armv8.1-m.main, you can use the +pacbti extension.

Use the optional extension name with -mcpu to disable the extensions that are not present in the CPU of your choice.

By default, -mfpu=auto and this enables the compiler to automatically select the floating-pointing and Advanced SIMD instructions based on the -mcpu option and extension.

#### -mfloat-abi:

If floating-point or Advanced SIMD instructions are present, then use the -mfloat-abi option to control the floating-point ABI, or use -mfloat-abi=soft to disable floating-point and Advanced SIMD instructions.

For the permissible values of -mfloat-abi, see the GCC online manual: https://gcc.gnu.org/onlinedocs/gcc-12.2.0/gcc/ARM-Options.html#index-mfloat-abi

#### -mthumb:

When using processors that can execute in Arm state and Thumb state, use -mthumb to generate code for Thumb state.

#### -mbranch-protection:

When using processors with the PACBTI extension, use -mbranch-protection=PROTECTION to select the type of branch protection to use.
When using PACBTI for Cortex-M processors with the PACBTI extension, PROTECTION can be:
  - none : Disable branch protection
  - bti [+ <pac_ret_clause>]
    -   bti :  Enable Branch Target Identification
    -   <pac_ret_clause> is:
        - pac-ret [+ <pac_ret_option>]
           - pac-ret : Enable return address signing and authentication for functions that save LR to the stack.
           - <pac_ret_option> is:
             - leaf : Enable return address signing and authentication for all leaf functions, including those that do not save LR to stack.
  - <pac-ret_clause> [+ bti]
  - standard : This is equivalent to -mbranch-protection=bti+pac-ret


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

**Example with PACBTI and no floating-point:**

    $ arm-none-eabi-gcc -march=armv8.1-m.main+pacbti -mfloat-abi=soft -mbranch-protection=standard

**Example with PACBTI, MVE, and floating-point with hard-float ABI:**

    $ arm-none-eabi-gcc -march=armv8.1-m.main+mve+pacbti -mfloat-abi=hard -mbranch-protection=standard

### Available multilibs

Arm GNU Toolchain 12.2.MPACBTI-Bet1 supports a set of multilibs in each toolchain.

To list all multilibs supported by any of the toolchain, use ```--print-multi-lib``` option. For example,

    $ arm-none-eabi-gcc --print-multi-lib

For the PACBTI extension, the following multilibs are supported:

    thumb/v8.1-m.main+pacbti/mbranch-protection/nofp
      This is used when building with  -march=armv8.1-m.main+pacbti -mbranch-protection=standard -mfloat-abi=soft

    thumb/v8.1-m.main+pacbti+fp/mbranch-protection/softfp
      This is used when building with  -march=armv8.1-m.main+pacbti+fp -mbranch-protection=standard -mfloat-abi=softfp

    thumb/v8.1-m.main+pacbti+fp/mbranch-protection/hard
      This is used when building with  -march=armv8.1-m.main+pacbti+fp -mbranch-protection=standard -mfloat-abi=hard

    thumb/v8.1-m.main+pacbti+dp/mbranch-protection/softfp
      This is used when building with -march=armv8.1-m.main+pacbti+fp.dp -mbranch-protection=standard -mfloat-abi=softfp

    thumb/v8.1-m.main+pacbti+dp/mbranch-protection/hard
      This is used when building with -march=armv8.1-m.main+pacbti+fp.dp -mbranch-protection=standard -mfloat-abi=hard

    thumb/v8.1-m.main+pacbti+mve/mbranch-protection/hard
      This is used when building with -march=armv8.1-m.main+pacbti+mve -mbranch-protection=standard -mfloat-abi=hard

To check which multilib is selected by the arm-none-eabi toolchain based on -mthumb, -mcpu, -mfpu and -mfloat-abi command line options:

    $ arm-none-eabi-gcc [-mthumb] -mcpu=CPU -mfpu=FPU -mfloat-abi=ABI --print-multi-dir

For example:

    $ arm-none-eabi-gcc -mcpu=cortex-a55 -mfpu=auto -mfloat-abi=hard --print-multi-dir
    thumb/v8-a+simd/hard

    $ arm-none-eabi-gcc -mcpu=cortex-r5 -mfpu=auto -mfloat-abi=softfp --print-multi-dir
    thumb/v7+fp/softfp

    $ arm-none-eabi-gcc -mcpu=cortex-m0 -mfpu=auto -mfloat-abi=soft --print-multi-dir
    thumb/v6-m/nofp

    $ arm-none-eabi-gcc -march=armv8.1-m.main+pacbti -mbranch-protection=standard -mfpu=auto -mfloat-abi=soft --print-multi-dir
    thumb/v8.1-m.main+pacbti/mbranch-protection/nofp

    $ arm-none-eabi-gcc -mcpu=cortex-m85 -mbranch-protection=standard -mfpu=auto -mfloat-abi=hard --print-multi-dir
    thumb/v8.1-m.main+pacbti+dp/mbranch-protection/hard


### C Libraries

*This section only applies for arm-none-eabi targets.*

Arm GNU Toolchain 12.2.MPACBTI-Bet1 is released with two prebuilt C libraries based on newlib, for arm-none-eabi target.

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

### Semi-hosting

Users can choose to use or not use semi-hosting by using the following instructions.

If you need semi-hosting, link as follows:

    $ arm-none-eabi-gcc --specs=rdimon.specs ${OTHER_LINK_OPTIONS}

If you don't need semi-hosting or if you use retarget, link as follows:

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


## Building Linux hosted toolchain from sources using Linaro's ABE

If you would like to build a toolchain yourself using the source revisions used for this release, you can do so  using Linaro ABE (Advanced Build Environment) and provided ABE manifest files.

Toolchains hosted on linux can be built using the steps provided below.

The example below shows how to build arm-gnu-toolchain-arm-none-eabi from sources using Linaro ABE build system.

### Instructions

**1. Install the dependencies**
ABE has a dependency on git-new-workdir and needs this tool to be installed in ```/usr/local/bin``` directory:

```
$ wget https://raw.githubusercontent.com/git/git/master/contrib/workdir/git-new-workdir
$ sudo mv git-new-workdir /usr/local/bin
$ sudo chmod +x /usr/local/bin/git-new-workdir
```

**2. Clone ABE from the URL below and checkout the stable branch (see Getting ABE):**

```
$ git clone https://git.linaro.org/toolchain/abe.git
```

**3. Create the build directory and change to it:**

```
$ mkdir build && cd build
```

**4. Configure ABE (from the build directory):**
```
$ ../abe/configure
```

**5. Download the toolchain manifest file:**

Download the toolchain manifest file arm-gnu-toolchain-arm-none-eabi-abe-manifest.txt from https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads, into the build folder:

```
$  wget https://developer.arm.com/-/media/Files/downloads/gnu/12.2.mpacbti-bet1/manifest/arm-gnu-toolchain-arm-none-eabi-abe-manifest.txt
```

**6. Build toolchain (from the build directory):**

```
$ ../abe/abe.sh --manifest arm-gnu-toolchain-arm-none-eabi-abe-manifest.txt --build all >& log &
```

**7. To build toolchain with newlib-nano configuration move out of build directory and create the build_newlib directory and change to it:**

```
$ cd .. && mkdir build_newlib && cd build_newlib
```

**8. Clone ABE from the URL below and checkout the stable branch (see Getting ABE):**

```
$ git clone https://git.linaro.org/toolchain/abe.git
```

**9. Configure ABE (from the build_newlib directory):**
```
$ abe/configure
```

**10. Download the toolchain manifest file:**

Download the toolchain manifest file arm-gnu-toolchain-arm-none-eabi-nano-abe-manifest.txt from https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads, into the build_newlib folder:

```
$  wget https://developer.arm.com/-/media/Files/downloads/gnu/12.2.mpacbti-bet1/manifest/arm-gnu-toolchain-arm-none-eabi-nano-abe-manifest.txt
```

**11. Build toolchain (from the build_newlib directory):**

```
$ abe/abe.sh --manifest arm-gnu-toolchain-arm-none-eabi-nano-abe-manifest.txt --build all >& log_nano
```

**12. Move out of newlib_nano directory and download the copy_nano_libraries.sh script:**

Download the copy_nano_libraries.sh script from https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads, to the folder above build_newlib directory:

```
$ cd .. && wget https://developer.arm.com/-/media/Files/downloads/gnu/12.2.mpacbti-bet1/manifest/copy_nano_libraries.sh
```

**13. Copy the newlib nano header and newlib nano libraries build in build_newlib folder to build folder and change to build folder:**

```
$ ./copy_nano_libraries.sh && cd build
```
The built arm-none-eabi toolchain will be installed and available for use in the builds/destdir/x86_64-pc-linux-gnu/bin/ directory.

---
