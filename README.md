[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE.md)


Lime Mingw fork
===============

This is a Mingw fork of Lime:
    
    https://github.com/openfl/lime


License
=======

Lime is free, open-source software under the [MIT license](LICENSE.md).


Installation
============

1 Clone repository

    git clone --recursive https://github.com/RetardMode/lime

2 Setup:

    haxelib dev lime lime
    
3 Make sure You have proper hxcpp configuration; build first for Win 32 bit (will be needed even for 64 bit targets):

    haxelib run lime rebuild windows -Dmingw
    
3a If hxcpp runs MSVC toolchain, try:

    haxelib run lime rebuild windows -Dmingw -Dtoolchain=mingw

4 Build for 64 bits:

    haxelib run lime rebuild windows -Dmingw -64 -DHXCPP_M64
    
5 Build projects with:

    haxelib run lime build windows -Dmingw -64


MinGW versions support
======================

32bit:
MinGW 4.8.2 from QT online installer

64bit:
MinGW-w64 recent version

TDM-GCC-64 recent version


Other versions
==============

Applications compiled with GCC-TDM-32 and MinGW-w64 targeting 32 bit architectures got segmentation fault in _pei386_runtime_relocator, which I guess is fault of those versions of MinGW itself.


Potential problems
==================

Q: If apps compiled with Mingw targeting 32 bit Win os don't work, why should I compile lime for 32 bit also?

A: Lime.ndll in 32 bits is needed for compilation script, even for 64 bit targets. Apps compiled with MinGW for 32 bits linked with 32 bit lime.ndll will probably not work, but library itself is working. But, if You have MSVC compiled lime.ndll for 32 bits from e.g. http://lib.haxe.org , You can put it into lime/ndll/Windows and don't have to recompile it with MinGW. With this You can compile for 32 bits with MSVC, and for 64 bits with MinGW. Or, You can put MinGW root with haxe libs folder into usb stick, and have portable native 64 bit toolkit.

Q: I've compiled lime for 32 and 64 bits with MinGW, and now compiling apps does not work. I got various errors about missing libs, what's wrong?

A: If You've comiled with MinGW-w64, lime.ndll will be linked with shared versions of lib-gcc and lib-stdc++. It should be that way, becouse linking those libraries statically will force You to follow GPL license for those libs, and in fact, in Your application. MinGW-w64 by default is linking those libs dynamically, but, as side effect, those libraries should be somewhere in Your PATH. Usually You will have Your Mingw bin folder in PATH, but if not, You may encounter various errors. Important thing to note is that, You need to have in PATH libraries for 32 bit, not for 64 bit. Build process uses 32 bit version of lime.ndll, so 32 bit versions of those libs should be accesible.

Q: So, for 64 bit target, shouldn't be 64 bit versions of gcc and std libs accesible also?

A: With proper configuration of hxcpp You should have those libs in folder 
    /Export/cpp/Windows/obj
Just copy them into 
    /Export/cpp/Windows/bin
folder, and App should work. Alternatively, You can copy missing libs from 64 bit MinGW root, or editing Your
    hxcpp/$(version)/toolchain/mingw-toolchain.xml
lines:
 
    <copyFile toolId="exe" name="libgcc_s_dw2-1.dll" from="${MINGW_ROOT}/bin" allowMissing="true" unless="no_shared_libs"/>

into:

    <copyFile toolId="exe" name="../bin/libgcc_s_dw2-1.dll" from="${MINGW_ROOT}/bin" allowMissing="true" unless="no_shared_libs"/>

etc.
