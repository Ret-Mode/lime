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

