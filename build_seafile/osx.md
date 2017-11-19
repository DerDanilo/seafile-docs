# Mac OS X

### Install QT 5.6.2:

* Download it from https://download.qt.io/archive/qt/5.6/5.6.2/qt-opensource-mac-x64-clang-5.6.2.dmg
* Double click the downloaded dmg file to start the installer, and install it to its default location.

## Install Macports

###Setup macports environment

1. Install xcode
  - Download Xcode from [website](https://developer.apple.com/xcode/downloads/) or
  [App Store](http://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12)

2. Install macports

  - Quick start https://www.macports.org/install.php

> visit https://www.macports.org/ for more

3. Install following libraries and tools using `port`

        sudo port install autoconf automake pkgconfig libtool glib2 \
        libevent vala openssl git jansson cmake

4. Install python

        sudo port install python27
        sudo port select --set python python27

        sudo port install py27-pip
        sudo port select --set pip pip27

5. Set pkg config environment

        export PKG_CONFIG_PATH=/opt/local/lib/pkgconfig:/usr/local/lib/pkgconfig
        export LIBTOOL=glibtool
        export LIBTOOLIZE=glibtoolize
        export CPPFLAGS="-I/opt/local/include"
        export LDFLAGS="-L/opt/local/lib -L/usr/local/lib -Wl,-headerpad_max_install_names"

        QT_BASE=$HOME/Qt5.6.2/5.6/clang_64
        export PATH=$QT_BASE/bin:$PATH
        export PKG_CONFIG_PATH=$QT_BASE/lib/pkgconfig:$PKG_CONFIG_PATH

Compiling libsearpc
------------------

Download [libsearpc](https://github.com/haiwen/libsearpc), then:

        ./autogen.sh
        ./configure
        make
        sudo make install

Compiling ccnet
---------------

Download [ccnet](https://github.com/haiwen/ccnet), then:

        ./autogen.sh
        ./configure
        make
        sudo make install

Compiling seafile
-----------------

1. Download [seafile](https://github.com/haiwen/seafile)
2. Compile

        ./autogen.sh
        ./configure --disable-fuse
        make
        sudo make install

Compiling seafile-client and packaging it
---------

1. execute the building script:

        ./scripts/build.py

2. Go to Release directory and see if `seafile-applet.app` can run correctly.

Problem you may encounter
-------------------------
1. If `install_name_tool` reports "malformed object" "unknown load command", It may be the version of xcode command line tools incompatible with `install_name_tool`.
2. If xcode can't find glib, Corrects xcode's "build settings/search paths/header search".
