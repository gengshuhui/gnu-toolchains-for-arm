Description
This is a release of GNU Toolchain 11.2-2022.02 for the Arm architecture. The release includes bare-metal and linux toolchains for various hosts, as described in the Host support section.

Features
This release is based on GCC 11.2.
Host support
Host support 

Description

Host identifier in the toolchain package name

Toolchain targets

Windows on IA-32 or x86_64	Windows 10 or later	mingw-w64-i686	
AArch64 Bare-metal

AArch64 Linux

AArch32 Bare-metal

AArch32 Linux hard-float

Linux on AArch64	
These toolchains are built on and for Ubuntu 18.04 on AArch64, and will likely also be useable on OS versions:

       - later than Ubuntu 18.04

       - RHEL8

aarch64	
AArch64 Bare-metal

AArch32 Bare-metal

AArch32  Linux hard-float

Linux on x86_64

These toolchains are built on and for RHEL7 on x86_64, and will likely also be useable on OS versions:

       - RHEL8 

       - Ubuntu 16.04 or later



x86_64	
AArch64 Bare-metal

AArch64  Linux

AArch64 Linux big-endian

AArch32 Bare-metal 

AArch32 Linux hard-float

Mac OS X on x86_64	
Mac OS X 10.15 or later 

Note: Toolchains described as [BETA] have not had the same level of testing as the other toolchains.

darwin-x86_64



[BETA] AArch64 Bare-metal

AArch32 Bare-metal

Changes since Arm release GCC 10.3-2021.07 and 10.3-2021.10
Updated GCC to version 11.2.
Updated Binutils to version 2.37.
Updated Glibc to version 2.34.
Updated GDB to version 11.
Sources
The sources for this release are provided in the source tar ball, gcc-arm-src-snapshot-11.2-2022.02.tar.xz, and includes the following items:

Component

Description

GCC 11.2	
Repository: git://gcc.gnu.org/git/gcc.git

Branch: refs/vendors/ARM/heads/arm-11

Revision:028202d8ad150f23fcccd4d923c96aff4c2607cf

Release note

glibc 2.34	
Repository: git://sourceware.org/git/glibc.git

Branch: master-2.34

Revision: 008003dc6e83439c5e04a744b7fd8197df19096e

Release note

newlib and newlib-nano based on 4.1.0	
Repository: git://sourceware.org/git/newlib-cygwin.git

Revision: 2a3a03972b35377aef8d3d52d873ac3b8fcc512c

binutils 2.37	
Repository: git://sourceware.org/git/binutils-gdb.git

Branch: binutils-2_37-branch

Revision: 5f62caec8175cf80a29f2bcab2c5077cbfae8c89

Release note

GDB 11	
Repository: git://sourceware.org/git/binutils-gdb.git

Branch: gdb-11-branch

Revision: a10d1f2c33a9a329f3a3006e07cfe872a7cc965b

Release note

libexpat 2.2.5	
Repository: https://github.com/libexpat/libexpat.git

Release note

 Linux Kernel	
Repository: git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git

Revision: v4.20.13

Release Note

libgmp 6.2
libisl 0.15
libmpfr 3.1.6
libmpc 1.0.3
libiconv 1.15

Sources are provided in release source tar ball.

Known dependencies
GDB's Python support requires Python 3.6 or libpython 3.6 installed on Linux hosts.
GDB's Python support requires Python DLL dependencies for Windows host.
Toolchains dedicated for Windows host require mingw-w64 library, a complete runtime environment for GCC.
The following executables in the Windows hosted toolchains:

 - aarch64-none-linux-gnu-dwp.exe

 - aarch64-none-linux-gnu-ld.gold.exe

 - arm-none-linux-gnueabihf-dwp.exe

 - arm-none-linux-gnueabihf-ld.gold.exe

have additional dependencies on the following dlls:

 - libwinpthread-1.dll

 - libgcc_s_sjlj-1.dll

 - libstdc++-6.dll

 - libgcc_s_dw2-1.dll

You can obtain the required dlls from the MinGW-W64 GCC-8.1.0 packages fromSourceForge:

- i686-posix-sjlj

- i686-posix-dwarf

The GNU Toolchains
The package names of the released GNU toolchain binaries have the following naming convention:

gcc-arm-<Release Version>-<Host>-<Target Triple>.tar.xz

For Windows, the binaries are provided in zip files and with installers.

For Linux, the binaries are provided as tarball files.

For Mac OS X, the binaries are provided as tarball files and pkg files.

Toolchain Package Name

Host OS

Target Description

gcc-arm-11.2-2022.02-aarch64-aarch64-none-elf.tar.xz	AArch64 Linux	AArch64 ELF bare-metal target.
gcc-arm-11.2-2022.02-aarch64-arm-none-eabi.tar.xz	AArch64 Linux	AArch32 bare-metal target.
gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf.tar.xz	AArch64 Linux	AArch32GNU/Linux target with hard float.
gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.zip

gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-eabi.exe

Windows	AArch32 bare-metal target.
gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.zip

gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-elf.exe

Windows	AArch64 ELF bare-metal target.
gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.zip

gcc-arm-11.2-2022.02-mingw-w64-i686-arm-none-linux-gnueabihf.exe

Windows	AArch32 GNU/Linux target with hard float.
gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.zip

gcc-arm-11.2-2022.02-mingw-w64-i686-aarch64-none-linux-gnu.exe

Windows	AArch64 GNU/Linux target.
gcc-arm-11.2-2022.02-x86_64-aarch64-none-elf.tar.xz	x86_64 Linux	AArch64 ELF bare-metal target.
gcc-arm-11.2-2022.02-x86_64-aarch64-none-linux-gnu.tar.xz	x86_64 Linux	AArch64 GNU/Linux target.
gcc-arm-11.2-2022.02-x86_64-aarch64_be-none-linux-gnu.tar.xz	x86_64 Linux	AArch64 GNU/Linux big-endian target.
gcc-arm-11.2-2022.02-x86_64-arm-none-eabi.tar.xz

x86_64 Linux	AArch32 bare-metal target.
gcc-arm-11.2-2022.02-x86_64-arm-none-linux-gnueabihf.tar.xz

x86_64 Linux	AArch32GNU/Linux target with hard float.
gcc-arm-11.2-2022.02-darwin-x86_64-aarch64-none-elf.tar.xz

gcc-arm-11.2-2022.02-darwin-x86_64-aarch64-none-elf.pkg

x86_64 Darwin	[BETA] AArch64 bare-metal target.
gcc-arm-11.2-2022.02-darwin-x86_64-arm-none-eabi.tar.xz

gcc-arm-11.2-2022.02-darwin-x86_64-arm-none-eabi.pkg

x86_64 Darwin	AArch32 bare-metal target.


Released files


gcc-arm-*.tar.xz	Toolchain binaries
gcc-arm-*.zip	Zipped toolchain binaries for Windows
gcc-arm-*.exe	Toolchain installer for Windows
gcc-arm-*.pkg	Toolchain installer for Mac
gcc-arm-src-snapshot-*.tar.xz	Toolchain sources
gcc-arm-src-snapshot-*-manifest.txt	Text manifest file with list of remote repositories for the toolchain
gcc-arm-*-abe-manifest.txt	Input files for the Linaro ABE build system.
*.asc	MD5 checksum files for sources and binaries
*.sha256asc	SHA256 checksum files for sources and binaries
Installation instructions
Extract XZ compressed release archive using TAR archiving utility:

   $ tar -xJf <toolchain binary> -C <destination directory>
Example for Linux(x86_64) hosted for AArch64 Linux target
   $ tar -xJf gcc-arm-11.2-2022.02-x86_64-aarch64-linux-gnu.tar.xz -C /path/to/destination/directory
Compute and check MD5 checksum of XZ compressed release archives using md5sum utility:

   $ md5sum --check gcc-arm-11.2-2022.02-x86_64-aarch64-linux-gnu.tar.xz.asc 
   gcc-arm-11.2-2022.02-x86_64-aarch64-linux-gnu.tar.xz: OK
The prebuilt binary bundles can be un-tarred and executed in place.  Unpack the Linux cross toolchain:

   $ mkdir install-lnx
   $ tar x -C install-lnx -f <filename>.tar.xz
   $ PATH=`pwd`/install-lnx/<filename>/bin:$PATH 
How to build the toolchain from sources
You can build Arm GNU Toolchain from sources using Linaro ABE (Advanced Build Environment) and provided ABE manifest files.

Below example shows how to build gcc-arm-aarch64-none-elf toolchain from sources using Linaro ABE build system.

Instructions
ABE has a dependency on git-new-workdir and needs this tool to be installed in /usr/local/bin directory:

        $ wget https://raw.githubusercontent.com/git/git/master/contrib/workdir/git-new-workdir

        $ sudo mv git-new-workdir /usr/local/bin

        $ sudo chmod +x /usr/local/bin/git-new-workdir 

Clone ABE from the URL below and checkout the stablebranch (see Getting ABE):

   $ git clone https://git.linaro.org/toolchain/abe.git
Create the build directory and change to it. Any name for the directory will work:

   $ mkdir build && cd build
Configure ABE (from the build directory):

   $ ../abe/configure
Download the toolchain manifest file, from https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/downloads, into the build folder, for the required toolchain, for example, gcc-arm-aarch64-none-elf-abe-manifest.txt:

   $  wget https://developer.arm.com/-/media/Files/downloads/gnu/11.2-2022.02/manifest/gcc-arm-aarch64-none-elf-abe-manifest.txt
Build toolchain (from the build directory):

   $ ../abe/abe.sh --manifest gcc-arm-aarch64-none-elf-abe-manifest.txt --build all
The built toolchain will be installed and available for use in the builds/destdir/x86_64-unknown-linux-gnu/bin/ directory.

Known issues
The macOS toolchains provided in the tar.xz format contain binaries that are not signed and notarized. To use signed and notarized binaries, use the macOS toolchains provided in the pkg format.

In the Windows and Linux hosted toolchains, GDB is provided with Python support. In the macOS hosted toolchains, GDB is provided without Python support.

If you install multiple Windows toolchains using the provided installer (.exe file), then only the last installed toolchain is visible in the Windows Add/Remove Programs menu. The other installed Windows toolchains can still be used or uninstalled by invoking the uninstaller from their respective install directories.

When you decompress the windows packages, the decompression requests permission to overwrite certain files. This is because the files have similar names with different case, which are treated as identical names on a Windows host. You can choose to overwrite the files with identical names.

Doing IPA on CMSE generates a linker error: The linker will error out when resulting object file contains a symbol for the clone function with the __acle_se prefix that has a non-local binding. Issue occurs when compiling binaries for M-profile Secure Extensions where the compiler may decide to clone a function with the cmse_nonsecure_entry attribute. Although cloning nonsecure entry functions is legal, as long as the clone is only used inside the secure application, the clone function itself should not be seen as a secure entry point and so it should not have the __acle_se prefix. A possible workaround for this is to add a 'noclone' attribute to functions with the 'cmse_nonsecure_entry'. This will prevent GCC from cloning such functions.

GCC can hang or crash if the input source code uses MVE Intrinsics polymorphic variants in a nested form. The depth of nesting that triggers this issue might vary depending on the host machine. This behaviour is observed when nesting 7 times or more on a high-end workstation. On less powerful machines, this behaviour might be observed with fewer levels of nesting. This issue is reported in https://gcc.gnu.org/bugzilla/show_bug.cgi?id=91937

Ask questions
For any questions, please use the Arm Communities forums.

Report bugs
Please report any bugs via the Linaro Bugzill