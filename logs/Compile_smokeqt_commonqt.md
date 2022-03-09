
```
$ git clone git@github.com:commonqt/smokeqt.git
$ cd smokeqt
$ mkdir build
$ cd build
$ cmake -DCMAKE_PREFIX_PATH="/opt/qt/qtbase/lib/cmake/Qt5;/usr/lib/llvm-11/lib/cmake/llvm;/opt/qt/smokegen/share/smoke/cmake" \
          -DCMAKE_C_COMPILER=clang-11 \
          -DCMAKE_CXX_COMPILER=clang++-11 ..
-- The C compiler identification is Clang 11.0.1
-- The CXX compiler identification is Clang 11.0.1
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /bin/clang-11 - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /bin/clang++-11 - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Build SMOKEQT5 bindings: QtGui;QtNetwork;QtPrintSupport;QtQml;QtQuick;QtWebChannel;QtWebEngineCore;QtWebEngineWidgets;QtWidgets
-- Skip SMOKEQT5 bindings:
-- Configuring done
-- Generating done
-- Build files have been written to: /home/hakon/test/smokeqt/build
hakon@hakon-Precision-7530:~/test/smokeqt/build$ make -j12
[  0%] Generating smokedata.cpp, x_1.cpp, x_2.cpp, x_3.cpp, x_4.cpp, x_5.cpp, x_6.cpp, x_7.cpp, x_8.cpp, x_9.cpp, x_10.cpp, x_11.cpp, x_12.cpp, x_13.cpp, x_14.cpp, x_15.cpp, x_16.cpp, x_17.cpp, x_18.cpp, x_19.cpp, x_20.cpp
using generator "/opt/qt/smokegen/bin/../lib/smokegen/generator_smoke.so"
didn't find file "/home/hakon/test/smokeqt/build/qtdefines"
parsing "/home/hakon/test/smokeqt/qtcore/qtcore_includes.h"
In file included from /home/hakon/test/smokeqt/qtcore/qtcore_includes.h:1:
In file included from /opt/qt/qtbase/include/QtCore/QtCore:6:
In file included from /opt/qt/qtbase/include/QtCore/qabstractanimation.h:43:
In file included from /opt/qt/qtbase/include/QtCore/qobject.h:47:
qobjectdefs-injected.moc:71:9: warning: 'Q_ENUM_IMPL' macro redefined [-Wmacro-redefined]
#define Q_ENUM_IMPL(ENUM) \
        ^
/opt/qt/qtbase/include/QtCore/qobjectdefs.h:113:9: note: previous definition is here
#define Q_ENUM_IMPL(ENUM) \
        ^
1 warning generated.
Generating SMOKE sources...
preparing SMOKE data [qtcore]
writing out smokedata.cpp [qtcore]
writing out x_*.cpp [qtcore]
Done.
Scanning dependencies of target smokeqtcore
[  3%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_3.cpp.o
[  4%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_2.cpp.o
[  4%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/smokedata.cpp.o
[  5%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_4.cpp.o
[  4%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_1.cpp.o
[  6%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_5.cpp.o
[  7%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_6.cpp.o
[  9%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_7.cpp.o
[  9%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_8.cpp.o
[ 10%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_10.cpp.o
[ 11%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_9.cpp.o
[ 12%] Building CXX object qtcore/CMakeFiles/smokeqtcore.dir/x_11.cpp.o
/home/hakon/test/smokeqt/build/qtcore/x_6.cpp/home/hakon/test/smokeqt/build/qtcore/x_4.cpp::/home/hakon/test/smokeqt/build/qtcore/x_7.cpp:33::1010:: 3fatal error : /home/hakon/test/smokeqt/build/qtcore/x_3.cpp:10: /home/hakon/test/smokeqt/build/qtcore/x_5.cpp/home/hakon/test/smokeqt/build/qtcore/x_1.cpp:fatal error:: 3'windows.h' file not found3::
1010'windows.h' file not found::
fatal errorfatal error: : 'windows.h' file not found'windows.h' file not found
#include <windows.h>

         ^~~~~~~~~~~
/home/hakon/test/smokeqt/build/qtcore/x_9.cpp#include <windows.h>#include <windows.h>:

3#include <windows.h>
:         ^~~~~~~~~~~10         ^~~~~~~~~~~
:
 fatal error: 'windows.h' file not found
#include <windows.h>
         ^~~~~~~~~~~
/home/hakon/test/smokeqt/build/qtcore/x_2.cpp:3:10: fatal error: 'windows.h' file not found
#include <windows.h>
         ^~~~~~~~~~~
/home/hakon/test/smokeqt/build/qtcore/x_8.cpp:3:10: fatal error: 'windows.h' file not found
#include <windows.h>
         ^~~~~~~~~~~
:3:10: fatal error: fatal error'windows.h' file not found
: #include <windows.h>
         ^~~~~~~~~~~
/home/hakon/test/smokeqt/build/qtcore/x_10.cpp:'windows.h' file not found3:10
#include <windows.h>
: fatal error: 'windows.h' file not found
         ^~~~~~~~~~~#include <windows.h>

         ^~~~~~~~~~~
         ^~~~~~~~~~~
/home/hakon/test/smokeqt/build/qtcore/x_11.cpp:3:10: fatal error: 'windows.h' file not found
#include <windows.h>
         ^~~~~~~~~~~
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:252: qtcore/CMakeFiles/smokeqtcore.dir/x_8.cpp.o] Error 1
make[2]: *** Waiting for unfinished jobs....
1 error generated.
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:174: qtcore/CMakeFiles/smokeqtcore.dir/x_2.cpp.o] Error 1
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:187: qtcore/CMakeFiles/smokeqtcore.dir/x_3.cpp.o] Error 1
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:239: qtcore/CMakeFiles/smokeqtcore.dir/x_7.cpp.o] Error 1
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:226: qtcore/CMakeFiles/smokeqtcore.dir/x_6.cpp.o] Error 1
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:278: qtcore/CMakeFiles/smokeqtcore.dir/x_10.cpp.o] Error 1
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:291: qtcore/CMakeFiles/smokeqtcore.dir/x_11.cpp.o] Error 1
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:200: qtcore/CMakeFiles/smokeqtcore.dir/x_4.cpp.o] Error 1
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:213: qtcore/CMakeFiles/smokeqtcore.dir/x_5.cpp.o] Error 1
1 error generated.
1 error generated.
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:161: qtcore/CMakeFiles/smokeqtcore.dir/x_1.cpp.o] Error 1
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:265: qtcore/CMakeFiles/smokeqtcore.dir/x_9.cpp.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:302: qtcore/CMakeFiles/smokeqtcore.dir/all] Error 2
make: *** [Makefile:149: all] Error 2
```
