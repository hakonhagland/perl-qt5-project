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

