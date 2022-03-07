# Building commonqt/smokegen

## Building and installing qtbase
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
$ ./configure -prefix /opt/qt/qtbase -opensource -release -nomake tests -nomake examples -c++std c++14 -no-dbus
```
### Configure summary
```
Build type: linux-g++ (x86_64, CPU features: mmx sse sse2)
Compiler: gcc 11.2.0
Configuration: sse2 aesni sse3 ssse3 sse4_1 sse4_2 avx avx2 avx512f avx512bw avx512cd avx512dq avx512er avx512ifma avx512pf avx512vbmi avx512vl compile_examples enable_new_dtags f16c largefile precompile_header rdrnd shani x86SimdAlways shared shared rpath release c++11 c++14 c++1z concurrent dbus reduce_exports reduce_relocations stl
Build options:
  Mode ................................... release
  Optimize release build for size ........ no
  Building shared libraries .............. yes
  Using C standard ....................... C11
  Using C++ standard ..................... C++17
  Using ccache ........................... no
  Using new DTAGS ........................ yes
  Relocatable ............................ yes
  Using precompiled headers .............. yes
  Using LTCG ............................. no
  Target compiler supports:
    SSE .................................. SSE2 SSE3 SSSE3 SSE4.1 SSE4.2
    AVX .................................. AVX AVX2
    AVX512 ............................... F ER CD PF DQ BW VL IFMA VBMI
    Other x86 ............................ AES F16C RDRAND SHA
    Intrinsics without -mXXX option ...... yes
  Build parts ............................ libs examples tools
Qt modules and options:
  Qt Concurrent .......................... yes
  Qt D-Bus ............................... yes
  Qt D-Bus directly linked to libdbus .... yes
  Qt Gui ................................. yes
  Qt Network ............................. yes
  Qt Sql ................................. yes
  Qt Testlib ............................. yes
  Qt Widgets ............................. yes
  Qt Xml ................................. yes
Support enabled for:
  Using pkg-config ....................... yes
  udev ................................... yes
  Using system zlib ...................... yes
  Zstandard support ...................... yes
Qt Core:
  DoubleConversion ....................... yes
    Using system DoubleConversion ........ no
  GLib ................................... yes
  iconv .................................. no
  ICU .................................... yes
  Built-in copy of the MIME database ..... yes
  Tracing backend ........................ <none>
  Logging backends:
    journald ............................. no
    syslog ............................... no
    slog2 ................................ no
  PCRE2 .................................. yes
    Using system PCRE2 ................... yes
Qt Network:
  getifaddrs() ........................... yes
  IPv6 ifname ............................ yes
  libproxy ............................... no
  Linux AF_NETLINK ....................... yes
  OpenSSL ................................ yes
    Qt directly linked to OpenSSL ........ no
  OpenSSL 1.1 ............................ yes
  DTLS ................................... yes
  OCSP-stapling .......................... yes
  SCTP ................................... no
  Use system proxies ..................... yes
  GSSAPI ................................. no
Qt Gui:
  Accessibility .......................... yes
  FreeType ............................... yes
    Using system FreeType ................ yes
  HarfBuzz ............................... yes
    Using system HarfBuzz ................ yes
  Fontconfig ............................. yes
  Image formats:
    GIF .................................. yes
    ICO .................................. yes
    JPEG ................................. yes
      Using system libjpeg ............... yes
    PNG .................................. yes
      Using system libpng ................ yes
  Text formats:
    HtmlParser ........................... yes
    CssParser ............................ yes
    OdfWriter ............................ yes
    MarkdownReader ....................... yes
      Using system libmd4c ............... no
    MarkdownWriter ....................... yes
  EGL .................................... yes
  OpenVG ................................. no
  OpenGL:
    Desktop OpenGL ....................... yes
    OpenGL ES 2.0 ........................ no
    OpenGL ES 3.0 ........................ no
    OpenGL ES 3.1 ........................ no
    OpenGL ES 3.2 ........................ no
  Vulkan ................................. yes
  Session Management ..................... yes
Features used by QPA backends:
  evdev .................................. yes
  libinput ............................... no
  INTEGRITY HID .......................... no
  mtdev .................................. no
  tslib .................................. no
  xkbcommon .............................. yes
  X11 specific:
    XLib ................................. yes
    XCB Xlib ............................. no
    EGL on X11 ........................... yes
QPA backends:
  DirectFB ............................... no
  EGLFS .................................. yes
  EGLFS details:
    EGLFS OpenWFD ........................ no
    EGLFS i.Mx6 .......................... no
    EGLFS i.Mx6 Wayland .................. no
    EGLFS RCAR ........................... no
    EGLFS EGLDevice ...................... no
    EGLFS GBM ............................ no
    EGLFS VSP2 ........................... no
    EGLFS Mali ........................... no
    EGLFS Raspberry Pi ................... no
    EGLFS X11 ............................ no
  LinuxFB ................................ yes
  VNC .................................... yes
  XCB:
    Using system-provided XCB libraries .. no
    XCB XKB .............................. no
    XCB XInput ........................... yes
    Native painting (experimental) ....... no
    GL integrations:
      GLX Plugin ......................... no
      EGL-X11 Plugin ..................... yes
Qt Sql:
  SQL item models ........................ yes
Qt Widgets:
  GTK+ ................................... yes
  Styles ................................. Fusion Windows
Qt PrintSupport:
  CUPS ................................... no
Qt Sql Drivers:
  DB2 (IBM) .............................. no
  InterBase .............................. no
  MySql .................................. yes
  OCI (Oracle) ........................... no
  ODBC ................................... no
  PostgreSQL ............................. no
  SQLite2 ................................ no
  SQLite ................................. yes
    Using system provided SQLite ......... no
  TDS (Sybase) ........................... no
Qt Testlib:
  Tester for item models ................. yes

Note: Also available for Linux: linux-clang linux-icc

Qt is now configured for building. Just run 'gmake'.
Once everything is built, you must run 'gmake install'.
Qt will be installed into '/opt/qt/qtbase'.

Prior to reconfiguration, make sure you remove any leftovers from
the previous build.

```
### install
```
$ make
$ sudo make install
```
## Building and installing qtdeclarative
```
$ export PREFIX=/opt/qt
$ git clone -b v5.14.2 git@github.com:qt/qtdeclarative.git
$ cd qtdeclarative
$ git switch -c v5.14.2
$ cat make.patch
```
```patch
diff --git a/src/qmldebug/qqmlprofilerevent_p.h b/src/qmldebug/qqmlprofilerevent_p.h
index a7e37d1964..3f13679a6a 100644
--- a/src/qmldebug/qqmlprofilerevent_p.h
+++ b/src/qmldebug/qqmlprofilerevent_p.h
@@ -49,6 +49,7 @@

 #include <initializer_list>
 #include <type_traits>
+#include <limits>

 //
 //  W A R N I N G
```
```
$ git apply make.patch
$ "$PREFIX"/qtbase/bin/qmake
$ qmake
```
### Configure summary:
```
Qt QML:
  QML network support .................... yes
  QML debugging and profiling support .... yes
  QML just-in-time compiler .............. yes
  QML sequence object .................... yes
  QML XML http request ................... yes
  QML Locale ............................. yes
Qt QML Models:
  QML list model ......................... yes
  QML delegate model ..................... yes
Qt Quick:
  Direct3D 12 ............................ no
  AnimatedImage item ..................... yes
  Canvas item ............................ yes
  Support for Qt Quick Designer .......... yes
  Flipable item .......................... yes
  GridView item .......................... yes
  ListView item .......................... yes
  TableView item ......................... yes
  Path support ........................... yes
  PathView item .......................... yes
  Positioner items ....................... yes
  Repeater item .......................... yes
  ShaderEffect item ...................... yes
  Sprite item ............................ yes

Qt is now configured for building. Just run 'make'.
Once everything is built, you must run 'make install'.
Qt will be installed into '/opt/qt/qtbase'.

Prior to reconfiguration, make sure you remove any leftovers from
the previous build.
```
### install
```
$ make
$ sudo make install
```
## Building and installing qtquickcontrols2
```
PREFIX=/opt/qt
git clone -b v5.14.2 git@github.com:qt/qtquickcontrols2.git
cd qtquickcontrols2
git switch -c v5.14.2
"$PREFIX"/qtbase/bin/qmake
make
sudo make install
```
## Building and installing qtwebchannel
```
PREFIX=/opt/qt
git clone -b v5.14.2 git@github.com:qt/qtwebchannel.git
cd qtwebchannel
git switch -c v5.14.2
"$PREFIX"/qtbase/bin/qmake
make
sudo make install
```
## Building and installing qtwebsockets
```
PREFIX=/opt/qt
git clone -b v5.14.2 git@github.com:qt/qtwebsockets.git
cd qtwebsockets
git switch -c v5.14.2
"$PREFIX"/qtbase/bin/qmake
make
sudo make install
```
## Building and installing qtwebengine
```

$ sudo apt-get install libnss3-dev protobuf-compiler libre2-dev \
     libsnappy-dev libjsoncpp-dev libwebp-dev libx11-xcb-dev
$ git clone -b v5.14.2 git@github.com:qt/qtwebengine.git
$ cd qtwebengine
$ git switch -c v5.14.2
$ git submodule update --init --progress
$ cd src/3rdparty/chromium
$ cat chromium.patch
```
```patch
diff --git a/chromium/media/cdm/supported_cdm_versions.h b/chromium/media/cdm/supported_cdm_versions.h
index 3f220da8c71..cddb2860f71 100644
--- a/chromium/media/cdm/supported_cdm_versions.h
+++ b/chromium/media/cdm/supported_cdm_versions.h
@@ -5,6 +5,7 @@
 #ifndef MEDIA_CDM_SUPPORTED_CDM_VERSIONS_H_
 #define MEDIA_CDM_SUPPORTED_CDM_VERSIONS_H_
 
+#include <cstddef>
 #include <array>
 
 #include "media/base/media_export.h"
diff --git a/chromium/third_party/blink/renderer/build/scripts/rule_bison.py b/chromium/third_party/blink/renderer/build/scripts/rule_bison.py
index f75e25fd23f..7e0767e951a 100755
--- a/chromium/third_party/blink/renderer/build/scripts/rule_bison.py
+++ b/chromium/third_party/blink/renderer/build/scripts/rule_bison.py
@@ -45,6 +45,19 @@ from utilities import abs
 
 from blinkbuild.name_style_converter import NameStyleConverter
 
+def modify_file(path, prefix_lines, suffix_lines, replace_list=[]):
+    prefix_lines = map(lambda s: s + '\n', prefix_lines)
+    suffix_lines = map(lambda s: s + '\n', suffix_lines)
+    with open(path, 'r') as f:
+        old_lines = f.readlines()
+    for i in range(len(old_lines)):
+        for src, dest in replace_list:
+            old_lines[i] = old_lines[i].replace(src, dest)
+    new_lines = prefix_lines + old_lines + suffix_lines
+    with open(path, 'w') as f:
+        f.writelines(new_lines)
+
+
 assert len(sys.argv) == 4 or len(sys.argv) == 5
 
 inputFile = abs(sys.argv[1])
@@ -115,3 +128,9 @@ print >>outputHFile, '#define %s' % headerGuard
 print >>outputHFile, outputHContents
 print >>outputHFile, '#endif  // %s' % headerGuard
 outputHFile.close()
+
+common_replace_list = [(inputRoot + '.hh',
+                        inputRoot + '.h')]
+modify_file(
+    outputCpp, [], [],
+    replace_list=common_replace_list)
diff --git a/chromium/third_party/breakpad/breakpad/src/client/linux/handler/exception_handler.cc b/chromium/third_party/breakpad/breakpad/src/client/linux/handler/exception_handler.cc
index b895f6d7ada..dc70527be3b 100644
--- a/chromium/third_party/breakpad/breakpad/src/client/linux/handler/exception_handler.cc
+++ b/chromium/third_party/breakpad/breakpad/src/client/linux/handler/exception_handler.cc
@@ -138,7 +138,7 @@ void InstallAlternateStackLocked() {
   // SIGSTKSZ may be too small to prevent the signal handlers from overrunning
   // the alternative stack. Ensure that the size of the alternative stack is
   // large enough.
-  static const unsigned kSigStackSize = std::max(16384, SIGSTKSZ);
+  static const unsigned kSigStackSize = std::max(16384L, SIGSTKSZ);
 
   // Only set an alternative stack if there isn't already one, or if the current
   // one is too small.
diff --git a/chromium/third_party/perfetto/include/perfetto/base/task_runner.h b/chromium/third_party/perfetto/include/perfetto/base/task_runner.h
index cf60401238f..da8a456619b 100644
--- a/chromium/third_party/perfetto/include/perfetto/base/task_runner.h
+++ b/chromium/third_party/perfetto/include/perfetto/base/task_runner.h
@@ -17,6 +17,7 @@
 #ifndef INCLUDE_PERFETTO_BASE_TASK_RUNNER_H_
 #define INCLUDE_PERFETTO_BASE_TASK_RUNNER_H_
 
+#include <cstdint>
 #include <functional>
 
 #include "perfetto/base/export.h"
diff --git a/chromium/third_party/webrtc/call/rtx_receive_stream.h b/chromium/third_party/webrtc/call/rtx_receive_stream.h
index 8ffa4400a9c..a389fc2a574 100644
--- a/chromium/third_party/webrtc/call/rtx_receive_stream.h
+++ b/chromium/third_party/webrtc/call/rtx_receive_stream.h
@@ -11,6 +11,7 @@
 #ifndef CALL_RTX_RECEIVE_STREAM_H_
 #define CALL_RTX_RECEIVE_STREAM_H_
 
+#include <cstdint>
 #include <map>
 
 #include "call/rtp_packet_sink_interface.h"
diff --git a/chromium/third_party/webrtc/modules/audio_processing/aec3/clockdrift_detector.h b/chromium/third_party/webrtc/modules/audio_processing/aec3/clockdrift_detector.h
index 22528c94892..cd5315a04ac 100644
--- a/chromium/third_party/webrtc/modules/audio_processing/aec3/clockdrift_detector.h
+++ b/chromium/third_party/webrtc/modules/audio_processing/aec3/clockdrift_detector.h
@@ -11,6 +11,7 @@
 #ifndef MODULES_AUDIO_PROCESSING_AEC3_CLOCKDRIFT_DETECTOR_H_
 #define MODULES_AUDIO_PROCESSING_AEC3_CLOCKDRIFT_DETECTOR_H_
 
+#include <cstddef>
 #include <array>
 
 namespace webrtc {
diff --git a/chromium/third_party/webrtc/modules/video_coding/decoding_state.h b/chromium/third_party/webrtc/modules/video_coding/decoding_state.h
index b87fb2d0345..ec972949d89 100644
--- a/chromium/third_party/webrtc/modules/video_coding/decoding_state.h
+++ b/chromium/third_party/webrtc/modules/video_coding/decoding_state.h
@@ -11,6 +11,7 @@
 #ifndef MODULES_VIDEO_CODING_DECODING_STATE_H_
 #define MODULES_VIDEO_CODING_DECODING_STATE_H_
 
+#include <cstdint>
 #include <map>
 #include <set>
 #include <vector>
```
### compile and install
```
$ git apply chromium.patch
$ cd ../../..
export PREFIX=/opt/qt
"$PREFIX"/qtbase/bin/qmake
make
sudo make install
```
## Building and installing qtsvg
```
PREFIX=/opt/qt
git clone -b v5.14.2 git@github.com:qt/qtsvg.git
cd qtsvg
git switch -c v5.14.2
"$PREFIX"/qtbase/bin/qmake
make
sudo make install
```

## Building smokegen
```
$ git clone git@github.com:commonqt/smokegen.git
$ cd smokegen
$ mkdir build
$ cmake .. -DCMAKE_INSTALL_PREFIX=/opt/qt/smokegen -DQt5_DIR=/opt/qt/qtbase -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_COMPILER=clang-13 -DCMAKE_CXX_COMPILER=clang++-13 -DCMAKE_PREFIX_PATH=/opt/qt/qtbase/lib/cmake/Qt5
-- The C compiler identification is Clang 13.0.0
-- The CXX compiler identification is Clang 13.0.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /bin/clang-13 - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /bin/clang++-13 - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found ZLIB: /usr/lib/x86_64-linux-gnu/libz.so (found version "1.2.11") 
-- Found LibXml2: /usr/lib/x86_64-linux-gnu/libxml2.so (found version "2.9.12") 
-- Found LLVM 13.0.0
-- Using LLVMConfig.cmake in: /lib/llvm-13/cmake
-- Linker detection: GNU ld
-- Configuring done
-- Generating done
-- Build files have been written to: /home/hakon/test/smokegen/build

$ make -j12
Scanning dependencies of target smokegen
Scanning dependencies of target smokebase
[  4%] Building CXX object smokebase/CMakeFiles/smokebase.dir/smokebase.cpp.o
[  9%] Building CXX object CMakeFiles/smokegen.dir/astconsumer.cpp.o
[ 13%] Building CXX object CMakeFiles/smokegen.dir/main.cpp.o
[ 22%] Building CXX object CMakeFiles/smokegen.dir/astvisitor.cpp.o
[ 27%] Building CXX object CMakeFiles/smokegen.dir/frontendaction.cpp.o
[ 27%] Building CXX object CMakeFiles/smokegen.dir/defaultargvisitor.cpp.o
[ 36%] Building CXX object CMakeFiles/smokegen.dir/options.cpp.o
[ 36%] Building CXX object CMakeFiles/smokegen.dir/type.cpp.o
[ 40%] Building CXX object CMakeFiles/smokegen.dir/ppcallbacks.cpp.o
[ 45%] Linking CXX shared library ../bin/libsmokebase.so
[ 45%] Built target smokebase
Scanning dependencies of target smokeapi
Scanning dependencies of target smokedeptool
[ 50%] Building CXX object smokeapi/CMakeFiles/smokeapi.dir/main.cpp.o
[ 54%] Building CXX object deptool/CMakeFiles/smokedeptool.dir/main.cpp.o
/home/hakon/test/smokegen/type.cpp:221:1: warning: non-void function does not return a value in all control paths [-Wreturn-type]
}
^
1 warning generated.
/home/hakon/test/smokegen/deptool/main.cpp:104:5: warning: 'qSort<QList<Smoke *>::iterator, bool (*)(Smoke *, Smoke *)>' is deprecated: Use std::sort [-Wdeprecated-declarations]
    qSort(smokeModules.begin(), smokeModules.end(), smokeModuleLessThan);
    ^
/opt/qt/qtbase/include/QtCore/qalgorithms.h:181:1: note: 'qSort<QList<Smoke *>::iterator, bool (*)(Smoke *, Smoke *)>' has been explicitly marked deprecated here
QT_DEPRECATED_X("Use std::sort") inline void qSort(RandomAccessIterator start, RandomAccessIterator end, LessThan lessThan)
^
/opt/qt/qtbase/include/QtCore/qglobal.h:294:33: note: expanded from macro 'QT_DEPRECATED_X'
#  define QT_DEPRECATED_X(text) Q_DECL_DEPRECATED_X(text)
                                ^
/opt/qt/qtbase/include/QtCore/qcompilerdetection.h:676:55: note: expanded from macro 'Q_DECL_DEPRECATED_X'
#    define Q_DECL_DEPRECATED_X(text) __attribute__ ((__deprecated__(text)))
                                                      ^
/home/hakon/test/smokegen/deptool/main.cpp:108:51: warning: 'toList' is deprecated: Use values() instead. [-Wdeprecated-declarations]
        QList<Smoke*> sortedList = parents[smoke].toList();
                                                  ^
/opt/qt/qtbase/include/QtCore/qset.h:250:5: note: 'toList' has been explicitly marked deprecated here
    QT_DEPRECATED_X("Use values() instead.")
    ^
/opt/qt/qtbase/include/QtCore/qglobal.h:294:33: note: expanded from macro 'QT_DEPRECATED_X'
#  define QT_DEPRECATED_X(text) Q_DECL_DEPRECATED_X(text)
                                ^
/opt/qt/qtbase/include/QtCore/qcompilerdetection.h:676:55: note: expanded from macro 'Q_DECL_DEPRECATED_X'
#    define Q_DECL_DEPRECATED_X(text) __attribute__ ((__deprecated__(text)))
                                                      ^
/home/hakon/test/smokegen/deptool/main.cpp:109:9: warning: 'qSort<QList<Smoke *>::iterator, bool (*)(Smoke *, Smoke *)>' is deprecated: Use std::sort [-Wdeprecated-declarations]
        qSort(sortedList.begin(), sortedList.end(), smokeModuleLessThan);
        ^
/opt/qt/qtbase/include/QtCore/qalgorithms.h:181:1: note: 'qSort<QList<Smoke *>::iterator, bool (*)(Smoke *, Smoke *)>' has been explicitly marked deprecated here
QT_DEPRECATED_X("Use std::sort") inline void qSort(RandomAccessIterator start, RandomAccessIterator end, LessThan lessThan)
^
/opt/qt/qtbase/include/QtCore/qglobal.h:294:33: note: expanded from macro 'QT_DEPRECATED_X'
#  define QT_DEPRECATED_X(text) Q_DECL_DEPRECATED_X(text)
                                ^
/opt/qt/qtbase/include/QtCore/qcompilerdetection.h:676:55: note: expanded from macro 'Q_DECL_DEPRECATED_X'
#    define Q_DECL_DEPRECATED_X(text) __attribute__ ((__depreecated__(text)))
                                                      ^
/home/hakon/test/smokegen/deptool/main.cpp:109:9: warning: 'qSort<QList<Smoke *>::iterator, bool (*)(Smoke *, Smoke *)>' is deprecated: Use std::sort [-Wdeprecated-declarations]
        qSort(sortedList.begin(), sortedList.end(), smokeModuleLessThan);
        ^
/opt/qt/qtbase/include/QtCore/qalgorithms.h:181:1: note: 'qSort<QList<Smoke *>::iterator, bool (*)(Smoke *, Smoke *)>' has been explicitly marked deprecated here
QT_DEPRECATED_X("Use std::sort") inline void qSort(RandomAccessIterator start, RandomAccessIterator end, LessThan lessThan)
^
/opt/qt/qtbase/include/QtCore/qglobal.h:294:33: note: expanded from macro 'QT_DEPRECATED_X'
#  define QT_DEPRECATED_X(text) Q_DECL_DEPRECATED_X(text)
                                ^
/opt/qt/qtbase/include/QtCore/qcompilerdetection.h:676:55: note: expanded from macro 'Q_DECL_DEPRECATED_X'
#    define Q_DECL_DEPRECATED_X(text) __attribute__ ((__deprecated__(text)))
                                                      ^
[ 59%] Linking CXX executable ../bin/smokeapi
3 warnings generated.
[ 63%] Linking CXX executable ../bin/smokedeptool
[ 63%] Built target smokeapi
[ 63%] Built target smokedeptool
/home/hakon/test/smokegen/astvisitor.cpp:530:96: error: no matching member function for call to 'toString'
                            tempArgType.setName(QString::fromStdString(args[i].getAsIntegral().toString(10)));
                                                                       ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~
/usr/lib/llvm-13/include/llvm/ADT/APSInt.h:82:8: note: candidate function not viable: no known conversion from 'int' to 'SmallVectorImpl<char> &' for 1st argument
  void toString(SmallVectorImpl<char> &Str, unsigned Radix = 10) const {
       ^
/usr/lib/llvm-13/include/llvm/ADT/APInt.h:1741:8: note: candidate function not viable: requires at least 3 arguments, but 1 was provided
  void toString(SmallVectorImpl<char> &Str, unsigned Radix, bool Signed,
       ^
/home/hakon/test/smokegen/astvisitor.cpp:530:72: error: reference to type 'const std::string' (aka 'const basic_string<char>') could not bind to an rvalue of type 'void'
                            tempArgType.setName(QString::fromStdString(args[i].getAsIntegral().toString(10)));
                                                                       ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/opt/qt/qtbase/include/QtCore/qstring.h:1506:58: note: passing argument to parameter 's' here
inline QString QString::fromStdString(const std::string &s)
                                                         ^
/home/hakon/test/smokegen/main.cpp:272:21: error: no member named 'mapVirtualFile' in 'clang::tooling::ToolInvocation'
                inv.mapVirtualFile(f->filename, { f->content, f->size });
                ~~~ ^
/home/hakon/test/smokegen/main.cpp:61:5: error: cannot use 'try' with exceptions disabled
    try
    ^
2 errors generated.
make[2]: *** [CMakeFiles/smokegen.dir/build.make:134: CMakeFiles/smokegen.dir/main.cpp.o] Error 1
make[2]: *** Waiting for unfinished jobs....
2 errors generated.
make[2]: *** [CMakeFiles/smokegen.dir/build.make:95: CMakeFiles/smokegen.dir/astvisitor.cpp.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:295: CMakeFiles/smokegen.dir/all] Error 2
make: *** [Makefile:149: all] Error 2
```
