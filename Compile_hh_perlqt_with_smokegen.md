```
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
-- Found Perl: /home/hakon/perlbrew/perls/perl-5.34.0/bin/perl (found version "5.34.0")
-- Found PerlLibs: /home/hakon/perlbrew/perls/perl-5.34.0/lib/5.34.0/x86_64-linux/CORE/libperl.a (found version "5.34.0")
CMake Error at /opt/qt/smokegen/share/smoke/cmake/SmokeConfig.cmake:30 (message):
  Could not find SmokeQtCore
Call Stack (most recent call first):
  /opt/qt/smokegen/share/smoke/cmake/SmokeConfig.cmake:57 (_print)
  /opt/qt/smokegen/share/smoke/cmake/SmokeConfig.cmake:98 (find_smoke_component)
  CMakeLists.txt:49 (find_package)

-- Configuring incomplete, errors occurred!
See also "/home/hakon/test/perlqt/build/CMakeFiles/CMakeOutput.log".
make: *** No targets specified and no makefile found.  Stop.
```
