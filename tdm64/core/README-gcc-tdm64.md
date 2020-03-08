                    ________________________________________
                  _/_                                      _\_
               __/__/  TDM-GCC Compiler Suite for Windows  \__\__
              | « « |             GCC 9 Series             | » » |
               ¯¯\¯¯\      MinGW-w64 64/32-bit Edition     /¯¯/¯¯
                  ¯\¯                                      ¯/¯
                    ¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯


This edition of TDM-GCC is a dual-arch multilib bootstrap of GCC's
x86_64-w64-mingw32 target, built to run on 32-bit or 64-bit Windows and generate
binaries for 32-bit or 64-bit Windows.


### BUGS: ###

If you encounter any bugs with this edition of TDM-GCC, it is likely that they
will be inherent to the x86_64-w64-mingw32 GCC target or to the MinGW-w64
runtime API. As such, you are encouraged to report bugs to the tracker for the
MinGW-w64 project on SourceForge (<https://sourceforge.net/p/mingw-w64/bugs/>).

Please note that the MinGW-w64 project also maintains easy-to-install GCC 64-bit
and 32-bit toolchains as part of [MSYS2](https://www.msys2.org/), and you are
encouraged to try them out as well to see if your problem exists on both
toolchains.

However, you may also submit a helpful bug report via
<http://tdm-gcc.tdragon.net/bugs>, though TDM-GCC is only supported on a minimal
best-effor basis.



««    INSTALLATION    »»
   ==================

## TDM/MINGW INSTALLER ##

Using the TDM/MinGW installer is highly recommended; it can automatically
install TDM-GCC (or the official MinGW GCC) as well as all supplementary base
system packages. The installer uses a standard wizard interface with reasonable
defaults.

## MANUAL INSTALLATION ##

Do not install TDM-GCC packages on top of a previous GCC installation of any
kind.

You will need to download and unpack a set of archives. A minimal base set of
archives is required; there are also some additional components that are
optional, adding support for additional programming languages or GCC features.

TDM-GCC provides a ZIP-compressed version and a TAR.XZ-compressed version of
each archive. Use whichever is easiest.

### REQUIRED BASE: ###
 * gcc-core
    * [gcc-9.2.0-tdm64-1-core.tar.xz]
 * binutils
    * [binutils-2.33.1-tdm64-1.tar.xz]
 * mingw64-runtime
    * [mingw64runtime-v7-git20191109-gcc9-tdm64-1.tar.xz]

### OPTIONAL: ###
 * gcc-c++ (gcc-9.2.0-tdm64-1-c++) - C++ support
 * gcc-ada (gcc-9.2.0-tdm64-1-ada) - Ada support
 * gcc-fortran (gcc-9.2.0-tdm64-1-fortran) - Fortran support
 * gcc-objc (gcc-9.2.0-tdm64-1-objc) - Objective-C/C++ support
 * gcc-openmp (gcc-9.2.0-tdm64-1-openmp) - OpenMP support
 * mingw32-make - GNU make for *-mingw32 GCC
    * [make-3.82.90-2-mingw32-cvs-20120902-bin.tar.lzma](http://prdownloads.sourceforge.net/mingw/make-3.82.90-2-mingw32-cvs-20120902-bin.tar.lzma?download)
    * [libintl-0.17-1-mingw32-dll-8.tar.xz](http://osdn.net/dl/mingw/libintl-0.18.3.2-2-mingw32-dll-8.tar.xz)
    * [libiconv-1.13.1-1-mingw32-dll-2.tar.lzma](http://osdn.net/dl/mingw/libiconv-1.14-4-mingw32-dll-2.tar.xz)
 * gdb (gdb-8.3.1-tdm64-1) - GNU source-level debugger, for x86_64-w64-mingw32
     GCC

You'll need GDB particularly if you want to use an IDE with debugging support.

Unpack all the archives to an empty directory. You may choose any path, though
it is recommended that you avoid a path with any spaces in the folder names.
Finally, consider adding the bin subdirectory to your Windows PATH environment
variable.


««    SUPPORT    »»
   =============

Support for the x86_64-w64-mingw32 GCC target, as well as for any
incompatibilities in its runtime API, is provided where possible by the
MinGW-w64 project. The MinGW-w64 project provides multiple venues for support
including a mailing list, an IRC channel, a web-based discussion forum on
SourceForge, and a web-based issue tracker on SourceForge.

For more information about MinGW-w64, see the project's home page at
<http://mingw-w64.sourceforge.net/>.

If you encounter a problem while using a TDM-GCC build that isn't present in a
previous MinGW-w64 MSYS2 or TDM release, please submit a helpful bug report! See
<http://tdm-gcc.tdragon.net/bugs> for instructions. Support for TDM-GCC is on a
low-priority best-effort basis.


««    USAGE NOTES    »»
   =================

## WINDOWS-DEFAULT-MANIFEST ##

As of release 9.2.0, both editions of TDM-GCC come with a
`windows-default-manifest` package. If you install it (which is recommended), it
provides an automatically-added XML compatibility manifest to all executables.
This internal manifest, `mingw32/lib/default-manifest.o`,  is designed to signal
to recent versions of Windows (8.1 and later) that the executable is compatible
with all versions of Windows and doesn't need to be run in a compatibility
environment for older versions.

If you provide your own manifest, it will override the default manifest.

The default manifest looks like this:

    LANGUAGE 0, 0

    /* CREATEPROCESS_MANIFEST_RESOURCE_ID RT_MANIFEST MOVEABLE PURE DISCARDABLE */
    1 24 MOVEABLE PURE DISCARDABLE
    BEGIN
    "<?xml version=""1.0"" encoding=""UTF-8"" standalone=""yes""?>\n"
    "<assembly xmlns=""urn:schemas-microsoft-com:asm.v1"" manifestVersion=""1.0"">\n"
    "  <trustInfo xmlns=""urn:schemas-microsoft-com:asm.v3"">\n"
    "    <security>\n"
    "      <requestedPrivileges>\n"
    "        <requestedExecutionLevel level=""asInvoker""/>\n"
    "      </requestedPrivileges>\n"
    "    </security>\n"
    "  </trustInfo>\n"
    "  <compatibility xmlns=""urn:schemas-microsoft-com:compatibility.v1"">\n"
    "    <application>\n"
    "      <!--The ID below indicates application support for Windows Vista -->\n"
    "      <supportedOS Id=""{e2011457-1546-43c5-a5fe-008deee3d3f0}""/>\n"
    "      <!--The ID below indicates application support for Windows 7 -->\n"
    "      <supportedOS Id=""{35138b9a-5d96-4fbd-8e2d-a2440225f93a}""/>\n"
    "      <!--The ID below indicates application support for Windows 8 -->\n"
    "      <supportedOS Id=""{4a2f28e3-53b9-4441-ba9c-d69d4a4a6e38}""/>\n"
    "      <!--The ID below indicates application support for Windows 8.1 -->\n"
    "      <supportedOS Id=""{1f676c76-80e1-4239-95bb-83d0f6d0da78}""/> \n"
    "      <!--The ID below indicates application support for Windows 10 -->\n"
    "      <supportedOS Id=""{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}""/> \n"
    "    </application>\n"
    "  </compatibility>\n"
    "</assembly>\n"
    END

See <https://sourceforge.net/p/mingw-w64/wiki2/default_manifest/> for more
details, and
<https://cygwin.com/git/?p=cygwin-apps/windows-default-manifest.git;a=tree> for
the upstream source, which is unmodified for TDM binaries.

## GDB AND GDB32: TDM BUILDS OF THE GNU DEBUGGER ##

The TDM "gdb" and "gdb32" packages are slightly-modified builds of GDB for
(respectively) 64-bit and 32-bit Windows that include Python 3, enable libstdc++
Python pretty printing by default, and use wrapper executables to allow 64-bit
and 32-bit cooperation in the "bin" directory. For more details, see the
separate README files (README-gdb32-tdm.md, README-gdb-tdm64.md).

## 32-BIT OR 64-BIT COMPILATION ##

In this edition of TDM-GCC, you can use "-m32" and "-m64" to control whether
32-bit or 64-bit binaries are generated. By default (if neither -m32 nor -m64 is
specified), 64-bit binaries will be generated.

 * In a 64-bit binary, all pointer math is 64-bit by default, and the built-in
   `size_t` and `ptrdiff_t` types are 64 bits in size (some other types are
   larger also).

 * Additionally, the following preprocessor definitions will be in effect:
    * `#define _WIN64 1` (also `WIN64`, `__WIN64`, and `__WIN64__`)
    * `#define __MINGW64__ 1`
    * `#define __x86_64 1` (also `__x86_64__`)
    * `#define __amd64 1` (also `__amd64__`)

Be sure to use "-m32" or "-m64" at both the compile stage and the link stage.

There are also two different exception handling mechanisms used in the generated
code, depending on whether you compile for 32-bit or 64-bit:

 * 32-bit programs compiled with this edition (TDM64) will use SJLJ (setjmp /
   longjmp) exception unwinding, which is somewhat compatible with Microsoft
   system DLLs and other MSVC-generated code. Cleanup code will not be executed
   when unwinding through MSVC function frames, you cannot throw C++ or other
   language-specific exceptions and have them caught in MSVC code, and you
   cannot catch C++ or other language-specific exceptions thrown by MSVC code.
   However, the exception unwinder can traverse MSVC function frames in the
   stack in order to reach GCC function frames.

 * 64-bit programs compiled with this edition (TDM64) will use 64-bit Windows
   SEH (Structured Exception Handling) exception unwinding, which has better
   MSVC compatibility. Cleanup code *will* be executed when unwinding through
   MSVC function frames, but you still can't catch language-specific exceptions
   from MSVC code or throw language-specific exceptions to MSVC code.

## POSIX THREADS, C++11 STD::THREAD AND OTHER SYNCHRONIZATION FEATURES ##

TDM-GCC includes a pthreads compatibility layer called "winpthreads".
"Winpthreads" is one of the libraries distributed by the MinGW-w64 project, and
it allows GCC to be compiled with full pthreads compatibility, which is
necessary to enable std::thread and other threading related functions in the C++
runtime.

Because of TDM-GCC's continuing goal of minimizing extra DLLs, winpthreads has
been compiled statically. It will be statically linked with every program you
compile, which will increase your baseline executable size.

The same mechanism used in libgcc and libstdc++ to allow EXEs and DLLs to share
state for handling exceptions has also been patched into winpthreads to allow
your EXEs and DLLs to share C++11 thread handles via the underlying pthread
handles.

Because every program you compile will now rely on winpthreads, you should make
sure to read and comply with its MIT-style license, included in the file
"COPYING.winpthreads.txt".

## LTO (LINK-TIME OPTIMIZATION) ##

For the TDM-GCC 9.2.0 release and later, GCC and binutils will interoperate
using the LTO plugin to automatically process code that was compiled with
`-flto`. Thus, you may mix code generated with LTO and code generated without.
See <http://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html> for further
details.

## EXCEPTIONS AND DLLS ##

> IMPORTANT NOTE:
> TDM-GCC uses a statically-linked libstdc++ by default! To use the libstdc++
> DLL, specify `-shared-libstdc++` on the command line.

The TDM releases of x86_64-w64-mingw32 GCC support propagating exceptions out
of shared libraries (DLLs) whether you use DLL versions or statically-linked
versions of the GCC runtime libraries. The statically-linked runtimes utilize
shared memory regions that will allow all TDM-GCC-compiled executables and DLLs
(for the same architecture) to propagate exceptions correctly. This method
incurs a small execution overhead as compared to the shared library method, but
has the very important benefit of not requiring you to redistribute extra DLLs
with your program.

By default, TDM-GCC creates executables and DLLs that use the statically-linked
runtimes, and does not require you to redistribute further DLLs. If you would
like to use the shared runtimes, you should add "-shared-libgcc" to the command
line, to use a shared version of libgcc, and additionally ensure that the shared
version of your language-specific runtime is being used. For C++, add
`-shared-libstdc++`.

You cannot use a shared version of libgcc with a static version of a language-
specific runtime. The reverse -- static libgcc with shared language-specific
runtime -- should work fine.

### GCC RUNTIME LICENSE ###

> There has been an update to the license exception clause that permits you to
> distribute programs that make use of the GCC runtime libraries without
> requiring you to license your programs under the GPLv3. As always, please be
> familiar with the terms of GCC's GPLv3 license and exception clauses, and do
> not redistribute any portion of GCC, including its runtime DLLs, in any way
> except as granted by the license. If you are unclear about which permissions
> are granted by the license, please consult a lawyer and/or the Free Software
> Foundation (<http://www.fsf.org/>).

A copy of the GPLv3 may be found in the file
COPYING-gcc-tdm.txt, and a copy of the runtime library exception clause may be
found in COPYING.RUNTIME-gcc-tdm.txt. In general, the runtime library exception
clause probably applies to any file found in the "lib" directory or its
subdirectories, and any DLL found in the "bin" directory -- but you should
consult the sources, available for download from the TDM-GCC project site on
SourceForge, if you are unsure.

## OPENMP AND WINPTHREADS ##

TDM-GCC has been built to allow the use of GCC's "-fopenmp" option for
generating parallel code as specified by the OpenMP API. (See
<http://gcc.gnu.org/onlinedocs/libgomp/> for details.) If you want to use
OpenMP in your programs, be sure to install the "openmp" optional package.

The OpenMP support in the TDM-GCC builds has received very little testing; if
you find build or packaging problems, please send a bug report (see BUGS above).

LibGOMP, GCC's implementation of OpenMP, currently only supports the use of the
POSIX Threads (pthreads) api for implementing its threading model. This edition
of TDM-GCC relies on the "winpthreads" library (part of the MinGW-w64 project
libraries and included in this distribution). The "winpthreads" library is
distributed under the terms of an MIT-style license; see
"COPYING.winpthreads.txt" for details.

In order to correctly compile code that utilizes OpenMP/libGOMP, you need to add
the "-fopenmp" option at compile time AND link time. By default, this will link
the static version of winpthreads to your program, and you should not need to
distribute any additional DLLs with your program. If you plan to distribute a
program that relies on OpenMP and winpthreads, be sure to understand and comply
with the terms of winpthreads' license (see COPYING.winpthreads.txt).

"libpthread.a" is included in the "lib" subdirectory of the openmp package along
with three other pthreads library files:
 - "libpthread_s.a" and "libwinpthread.dll.a" link to a DLL version of
     winpthreads - libwinpthread-1.dll.
 - "libwinpthread.a" is the same as "libpthread.a".

## WARNINGS AND ERRORS ##

Recent GCC releases make significant strides in optimization capabilities, error
detection, and standards compliance. For you, the end user, this often means
that code which compiled and ran without problems on previous GCC releases will
exhibit some warnings and maybe even a few errors.

These meaningful warnings and errors are a very good thing, as they help the
programmer to write safer and more correct code. Unfortunately, there's also a
chance you might encounter incorrect warnings or errors, ICE's (internal
compiler errors, where the compiler makes a mistake and has to bail out), or
even miscompilations (where your code is incorrectly compiled and produces the
wrong result).

If you encounter an ICE while using a TDM-GCC build, feel free to file a bug
report (see BUGS above). With any other unexpected problem, you are urged to
work from the assumption that it stems from user error, and ensure that your
code is correct and standards-compliant.


««    DETECTION AND COMPATIBILITY (TDM64)    »»
   =========================================

You can detect the operation of TDM64 GCC by parsing the GCC `--version` string,
which will include "(tdm64-n)" in the output, where n is a number indicating how
many TDM64 binary releases were made against a given upstream GCC release.
TDM-GCC does not otherwise attempt to identify itself at compile time, such as
with preprocessor defines.

Ideally, the binaries and compiled code produced by TDM-GCC would be
ABI-compatible with other Windows compilers, such as MinGW.org, MinGW-w64/MSYS2,
and even Microsoft Visual C/C++. This is sadly not the case.

* Generated code:
  * [MAYBE: MinGW.org, `mingw32`]
    * You might be able to mix .o and .a files with C linkage from MinGW.org GCC
      and TDM-GCC `-m32`, as long as the major versions match. Don't try it with
      exceptions.
  * [MAYBE: MinGW-w64, `i686-w64-mingw32`]
    * The `-m32` code from this TDM64 edition should be compatible with C code
      from the same major GCC version, and C++ code from the same major+minor
      GCC version. It should work with exceptions, when both toolchains are
      **SJLJ**.
  * [MAYBE: MinGW-w64, `x86_64-w64-mingw32`]
    * The normal 64-bit code from this TDM64 edition should be compatible with C
      code from the same major GCC version, and C++ code from the same
      major+minor GCC version, including exceptions.
  * [NO: MSVC]
    * Microsoft Visual C/C++ generated code is not compatible with GCC unless
      you are truly elite.
* DLL linkage:
  * [MAYBE: MinGW.org, MinGW-w64]
    * TDM-GCC builds DLLs and EXEs with statically-linked libgcc and libstdc++,
      that rely on a shared memory region to propagate exceptions.
    * Linking DLLs to EXEs with C linkage (extern "C", __cdecl, __stdcall,
      __fastcall) is generally safe regardless of maintainer, GCC version, or
      exception flavor.
    * If you pass the `-shared-libgcc` and `-shared-libstdc++` flags to TDM-GCC,
      it will built DLLs and EXEs that depend on the libgcc and libstdc++ DLLs.
      A DLL or EXE built with these options can safely link to a MinGW.org or
      MinGW-w64 DLL or EXE and pass exceptions into and out of DLLs, if the
      other GCC and TDM-GCC share the same GCC libstdc++ ABI. The ABI may change
      between GCC minor releases. 32-bit and 64-bit DLLs and EXEs mostly cannot interoperate.
    * If you link a normal TDM-GCC-built DLL to a MinGW.org-built or
      MinGW-w64-built EXE, you must distribute the TDM versions of the libgcc
      and libstdc++ DLLs. These versions will track the shared memory region and
      allow exceptions to propagate between DLL and EXE. The same goes for
      linking a MinGW.org or MinGW-w64 DLL to a normal non-shared TDM-GCC EXE.
  * [WITH CARE: MSVC]
    * If you take care to match calling conventions and catch exceptions, C
      linkage is possible. C++ linkage for classes is fraught and for STL /
      libstdc++ objects is not possible. Maybe there's a compatibility layer
      somewhere.
* `libgcc` and `libstdc++` DLL replaceability:
  * The 32-bit libgcc DLL distributed with TDM64 GCC is expected to be ABI
    compatible with other 32-bit libgcc DLLs in the same GCC major release
    series. The 32-bit libstdc++ DLL distributed with TDM32 GCC is expected to
    be ABI compatible with other 32-bit MinGW-w64 libstdc++ DLLs in the same
    major+minor release series.
  * The 64-bit DLLs, aside from having _64 appended to their name, are expected
    to be ABI compatible according to the same rules as the 32-bit DLLs.


««    BUGS AND KNOWN ISSUES    »»
   ===========================

As these builds are provided on the same basis as the source releases, and the
mingw32 target in GCC tends to receive somewhat less-than-average attention,
some bugs are expected. If you encounter a bug that you are certain is in the
GCC sources (such as an ICE), or that is due to an issue in the building or
packaging process, you are encouraged to report it. Please visit the TDM-GCC
Bugs page at <http://tdm-gcc.tdragon.net/bugs> for bug reporting instructions.


««    LOCAL FIXES AND CHANGES    »»
   =============================

See the [Github repository](https://github.com/jmeubank/tdm-gcc-src) for more details.

+ Fix-using-large-PCH.patch                                    # Handle larger precompiled headers
+ make-rel-pref.patch                                          # Make GCC fully portable (relocatable)
+ lfs.patch                                                    # Enable large file support in libstdc++
+ libgomp.patch                                                # Allow libgomp to interoperate with user-generated pthreads
+ libgcceh.patch                                               # Reintegrate libgcc_eh into libgcc
+ defstatic.patch                                              # Make static versions of libgcc and libstdc++ the default, instead of the shared versions
+ ada-lfs.patch                                                # Allow Ada to build for older versions of the MSVCRT without a stat64 equivalent
+ relocate.patch                                               # Make GCC fully relocatable, not searching any fixed paths
+ eh_shmem.patch                                               # Create a shared memory handle to allow exceptions from DLLs without shared GCC DLLs
+ threads.patch                                                # Support winpthreads for the 32-bit mingw32 target and a static version of winpthreads
+ more-gnattools.patch                                         # Enable building gnatdll for mingw* targets
+ windows-lrealpath.patch                                      # Allow forward slashes in libiberty as path separators on Windows
+ mutex-leak.patch                                             # Fix memory leak when using C++11 mutexes
+ xmmintrin.patch                                              # Add C++ include guards to xmmintrin.h
+ crtbegin.patch                                               # Remove static modifier from `__EH_FRAME_BEGIN__`
+ gnat-implibs.patch                                           # Create import libraries for the DLL versions of libgnat and libgnarl
+ mingw-ansi-stdio.patch                                       # MinGW.org ANSI stdio definition fix
+ mcrtdll.patch                                                # Allow specifying newer MSVCRT versions with -mcrtdll=
+ dw2-reg-frame.patch                                          # Prevent DW2 frame register/unregister from getting mistakenly stripped
+ libgfortran.patch                                            # Allow libgfortran to use umask semantics on MinGW64 but not on MinGW32
+ mingw32-float.h.patch                                        # Fix inclusion of GCC float.h before MinGW.org float.h
+ ssp-wincrypt.patch                                           # Include wincrypt.h for libssp
+ ada-unicode.patch                                            # Fix the include and define order in ada headers to allow Unicode TCHAR detection to work under MinGW.org
+ mingw-wformat.patch                                          # Add MinGW-specific format attributes to GCC's formatted printf checking
+ mingw32-ada-socket.patch                                     # Fix headers so that winsock constants are correctly found and used in Ada runtime.
+ libobjc-install.patch                                        # Allow the libobjc DLL to be stripped when installed
+ Relocate-libintl.patch                                       # Makes libintl resources in Windows binaries automatically relocatable
+ branch-clone_function_name_1-Retain-any-stdcall-suffix.patch # Preserve stdcall @n suffixes at the end of function names when cloning
+ libstdc__-in-out.patch                                       # Don't use Microsoft-reserved `__in` or `__out` as variable names
+ fix-libatomic-building-for-threads-win32.patch               # Build libatomic with pthreads on Windows
+ ktietz-libgomp.patch                                         # Zero allocated memory in libgomp and run DejaGNU tests if desired
+ gcc-libgomp-ftime64.patch                                    # Use 64-bit ftime in libgomp
+ buildsys.patch                                               # Minor build system hacks for building TDM-GCC in MSYS
+ diagnostic-color.patch                                       # Emit colors in GCC diagnostics when running under MinTTY
+ Handle-spaces-in-path-for-default-manifest.patch             # Allow spaces in specfile entries that expand to full paths if they are library files
+ Windows-Follow-Posix-dir-exists-semantics-more-close.patch   # From 9f49390e2cd9085ca1cc03906a146861dbe8135f Mon Sep 17 00:00:00 2001
+ Windows-Don-t-ignore-native-system-header-dir.patch          # From a2bc77d0e198659e72c9addb89a993007de99fe7 Mon Sep 17 00:00:00 2001
+ stdcxx-mingw32.patch                                         # Fixes for building libstdc++ under MinGW.org API
+ libs64.patch                                                 # Append "_64" to names of 64-bit runtime DLLs



««    SOURCE CODE    »»
   =================

The source code for the TDM-GCC binary releases is available on Github:
 * gcc: https://github.com/jmeubank/tdm-gcc-src/tree/tdm-patches.public
 * winpthreads: https://github.com/jmeubank/tdm-winpthreads/tree/tdm-patches.public
 * gdb: https://github.com/jmeubank/tdm-binutils-gdb/tree/tdm-patches-gdb.public

Each of the above repositories contains a `_PATCHES` folder containing the
patches that were applied to the most recent TDM releases.

 * The TDM-GCC installer: https://github.com/jmeubank/tdm-gcc-installer
 * The scripts that drive the builds: https://github.com/jmeubank/tdm-gccmaster-scripts


««    COMPONENT LICENSES    »»
   =================

This edition of TDM-GCC is comprised of several distinct parts with respect to
licensing, namely:
 * GCC proper and its various language components,
 * The GNU binutils package, and
 * The MinGW-w64 runtime API.

The GCC proper packages in TDM-GCC contain binary distributions constituting a
work based on GCC, ISL, MPC, libiconv, GMP, MPFR, and winpthreads.

* GCC itself is licensed under the GPLv3; for further details, see
  "COPYING3-gcc-tdm.txt". GCC's runtime libraries are licensed with an
  additional exception clause; see "COPYING.RUNTIME-gcc-tdm.txt".

* MPC, libiconv, GMP, and MPFR are each licensed under the LGPLv3, a somewhat
  more permissive version of the GPL; see "COPYING3.LIB-gcc-tdm.txt".

* ISL and winpthreads use an "MIT-style" license, reproduced in
  "COPYING.ISL.txt" and "COPYING.winpthreads.txt".

The GNU binutils package is a binary distribution licensed under the GPLv3; see
"COPYING3-gcc-tdm.txt".

The MinGW-w64 runtime API includes binary and source files that fall under a
variety of licenses (all of which are "GPLv3 compatible"); for further details,
see "COPYING.MinGW-w64.txt" (for non-runtime portions) and
"COPYING.MinGW-w64-runtime.txt" (for the runtime only).
