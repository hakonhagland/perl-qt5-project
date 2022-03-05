# Researching previous work

- [KDE TechBase: Languages/Perl](https://techbase.kde.org/Languages/Perl)
- [Google Code archive, August 10, 2010: perlqt4](https://code.google.com/archive/p/perlqt4/)
- [2003, PerlQt version 3, PerlQt Project](http://perlqt.sourceforge.net/)

# About SMOKE (does not support Qt5)

- [KDE TechBase: Languages/Smoke](https://techbase.kde.org/Languages/Smoke)

- [time to retire some kde4/smoke-based language bindings?](https://devel.fedoraproject.narkive.com/wcw8K9x3/time-to-retire-some-kde4-smoke-based-language-bindings)

- [Ruby bindings to Qt: development of the upstream qtruby/smoke has ended](https://github.com/ryanmelt/qtbindings/issues/131)

- [Ruby binding to Qt: project is no longer maintained](https://github.com/ryanmelt/qtbindings)

 It only supports Qt4 which the latest linux distributions no longer
 include in their package repos. No future releases or changes are
 planned. If you would like to take over, please fork, and make the
 changes to support Qt5/Qt6. This will be really difficult as the
 Smoke libraries used in this project do not work well with C++11+

# Compiling smokegen

- Refer to [chrisburel/smokegen](https://github.com/chrisburel/smokegen)
- Current compile error:
```
$ cmake -DCMAKE_INSTALL_PREFIX=/opt/perlqt -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ ..
$ make -j12
Scanning dependencies of target smokegen
[  9%] Built target smokebase
[ 27%] Built target smokeapi
[ 27%] Built target smokedeptool
[ 36%] Building CXX object CMakeFiles/smokegen.dir/frontendaction.cpp.o
[ 36%] Building CXX object CMakeFiles/smokegen.dir/astvisitor.cpp.o
[ 40%] Building CXX object CMakeFiles/smokegen.dir/main.cpp.o
/home/hakon/test/smokegen/astvisitor.cpp:484:96: error: no matching member function for call to 'toString'
                            tempArgType.setName(QString::fromStdString(args[i].getAsIntegral().toString(10)));
                                                                       ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~
/usr/lib/llvm-13/include/llvm/ADT/APSInt.h:82:8: note: candidate function not viable: no known conversion from 'int' to 'SmallVectorImpl<char> &' for 1st argument
  void toString(SmallVectorImpl<char> &Str, unsigned Radix = 10) const {
       ^
/usr/lib/llvm-13/include/llvm/ADT/APInt.h:1741:8: note: candidate function not viable: requires at least 3 arguments, but 1 was provided
  void toString(SmallVectorImpl<char> &Str, unsigned Radix, bool Signed,
       ^

```
