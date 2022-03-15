```
$ cd build/
$ cmake -DCMAKE_INSTALL_PREFIX=/opt/qt/smokeqt \
          -DCMAKE_PREFIX_PATH="/opt/qt/qtbase/lib/cmake/Qt5;/usr/lib/llvm-11/lib/cmake/llvm;/opt/qt/smokegen/share/smoke/cmake" \
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

$ make VERBOSE=1
/usr/bin/cmake -S/home/hakon/test/smokeqt -B/home/hakon/test/smokeqt/build --check-build-system CMakeFiles/Makefile.cmake 0
/usr/bin/cmake -E cmake_progress_start /home/hakon/test/smokeqt/build/CMakeFiles /home/hakon/test/smokeqt/build//CMakeFiles/progress.marks
make  -f CMakeFiles/Makefile2 all
make[1]: Entering directory '/home/hakon/test/smokeqt/build'
make  -f qtcore/CMakeFiles/smokeqtcore.dir/build.make qtcore/CMakeFiles/smokeqtcore.dir/depend
make[2]: Entering directory '/home/hakon/test/smokeqt/build'
[  0%] Generating smokedata.cpp, x_1.cpp, x_2.cpp, x_3.cpp, x_4.cpp, x_5.cpp, x_6.cpp, x_7.cpp, x_8.cpp, x_9.cpp, x_10.cpp, x_11.cpp, x_12.cpp, x_13.cpp, x_14.cpp, x_15.cpp, x_16.cpp, x_17.cpp, x_18.cpp, x_19.cpp, x_20.cpp
cd /home/hakon/test/smokeqt/build/qtcore && /opt/qt/smokegen/bin/smokegen -p 20 -config /home/hakon/test/smokeqt/build/qtcore/config.xml -smokeconfig /home/hakon/test/smokeqt/qtcore/smokeconfig.xml -L /home/hakon/test/smokeqt/build -clangOptions -fPIC -std=c++11 -- /home/hakon/test/smokeqt/qtcore/qtcore_includes.h
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
Illegal instruction (core dumped)
make[2]: *** [qtcore/CMakeFiles/smokeqtcore.dir/build.make:82: qtcore/smokedata.cpp] Error 132
make[2]: Leaving directory '/home/hakon/test/smokeqt/build'
make[1]: *** [CMakeFiles/Makefile2:301: qtcore/CMakeFiles/smokeqtcore.dir/all] Error 2
make[1]: Leaving directory '/home/hakon/test/smokeqt/build'
make: *** [Makefile:149: all] Error 2
```
