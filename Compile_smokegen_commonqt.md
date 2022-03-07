# Building commonqt/smokegen

```
$ sudo apt-get install libclang-11-dev libclang-13-dev llvm-11-dev llvm-13-dev
$ g++ --version | head -1
g++ (Ubuntu 11.2.0-7ubuntu2) 11.2.0
$ clang --version
Ubuntu clang version 13.0.0-2
Target: x86_64-pc-linux-gnu
Thread model: posix
InstalledDir: /bin
$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 21.10
Release:	21.10
Codename:	impish
$ git clone -b v5.14.2 git@github.com:qt/qtbase.git
$ git switch -c v5.14.2
$ cat configure.patch
```

```patch
diff --git a/src/corelib/global/qfloat16.h b/src/corelib/global/qfloat16.h
index 02fd2f03cc..1bde205c92 100644
--- a/src/corelib/global/qfloat16.h
+++ b/src/corelib/global/qfloat16.h
@@ -44,6 +44,7 @@
 #include <QtCore/qglobal.h>
 #include <QtCore/qmetatype.h>
 #include <string.h>
+#include <limits>

 #if defined(QT_COMPILER_SUPPORTS_F16C) && defined(__AVX2__) && !defined(__F16C__)
 // All processors that support AVX2 do support F16C too. That doesn't mean
diff --git a/src/corelib/text/qbytearraymatcher.h b/src/corelib/text/qbytearraymatcher.h
index 0eedfc1d20..ee415e336d 100644
--- a/src/corelib/text/qbytearraymatcher.h
+++ b/src/corelib/text/qbytearraymatcher.h
@@ -41,6 +41,7 @@
 #define QBYTEARRAYMATCHER_H

 #include <QtCore/qbytearray.h>
+#include <limits>

 QT_BEGIN_NAMESPACE
```

```
$ git apply configure.patch
$ ./configure -prefix /opt/qt/qtbase -opensource -release -nomake tests -nomake examples -c++std c++14 -no-dbus -prefix /opt/qt/qtbase
$ make
$ make install
```

