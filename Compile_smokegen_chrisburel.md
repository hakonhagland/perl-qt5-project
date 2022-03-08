```
$ git clone git@github.com:chrisburel/smokegen.git
$ cd smokegen
$ mkdir build
$ cd build
$ cmake .. -DCMAKE_INSTALL_PREFIX=/opt/qt/smokegen \
    -DCMAKE_PREFIX_PATH="/opt/qt/qtbase/lib/cmake/Qt5;/usr/lib/llvm-11/lib/cmake/llvm" \
    -DQt5_DIR=/opt/qt/qtbase -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_C_COMPILER=clang-11 -DCMAKE_CXX_COMPILER=clang++-11
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
-- Found LLVM 11.0.1
-- Using LLVMConfig.cmake in: /usr/lib/llvm-11/lib/cmake/llvm
-- Linker detection: GNU ld
-- Configuring done
-- Generating done
-- Build files have been written to: /home/hakon/test/smokegen/build

$ make -j12
Scanning dependencies of target smokebase
Scanning dependencies of target smokegen
[  4%] Building CXX object smokebase/CMakeFiles/smokebase.dir/smokebase.cpp.o
[ 13%] Building CXX object CMakeFiles/smokegen.dir/frontendaction.cpp.o
[ 13%] Building CXX object CMakeFiles/smokegen.dir/defaultargvisitor.cpp.o
[ 18%] Building CXX object CMakeFiles/smokegen.dir/main.cpp.o
[ 22%] Building CXX object CMakeFiles/smokegen.dir/astconsumer.cpp.o
[ 27%] Building CXX object CMakeFiles/smokegen.dir/astvisitor.cpp.o
[ 36%] Building CXX object CMakeFiles/smokegen.dir/ppcallbacks.cpp.o
[ 36%] Building CXX object CMakeFiles/smokegen.dir/type.cpp.o
[ 40%] Building CXX object CMakeFiles/smokegen.dir/options.cpp.o
[ 45%] Linking CXX shared library ../bin/libsmokebase.so
[ 45%] Built target smokebase
Scanning dependencies of target smokedeptool
Scanning dependencies of target smokeapi
[ 50%] Building CXX object deptool/CMakeFiles/smokedeptool.dir/main.cpp.o
[ 54%] Building CXX object smokeapi/CMakeFiles/smokeapi.dir/main.cpp.o
/home/hakon/test/smokegen/ppcallbacks.cpp:17:29: error: member access into incomplete type 'const clang::FileEntry'
    llvm::StringRef name = F->getName();
                            ^
/usr/lib/llvm-11/include/clang/Basic/SourceLocation.h:356:7: note: forward declaration of 'clang::FileEntry'
class FileEntry;
      ^
1 error generated.
make[2]: *** [CMakeFiles/smokegen.dir/build.make:160: CMakeFiles/smokegen.dir/ppcallbacks.cpp.o] Error 1
make[2]: *** Waiting for unfinished jobs....
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
#    define Q_DECL_DEPRECATED_X(text) __attribute__ ((__deprecated__(text)))
                                                      ^
3 warnings generated.
[ 59%] Linking CXX executable ../bin/smokedeptool
[ 63%] Linking CXX executable ../bin/smokeapi
[ 63%] Built target smokedeptool
[ 63%] Built target smokeapi
/home/hakon/test/smokegen/astvisitor.cpp:579:53: error: no matching constructor for initialization of 'clang::AnnotateAttr'
                                    auto annotate = clang::AnnotateAttr(clang::SourceRange(), *ctx, llvm::StringRef("qt_property"), 0).clone(*ctx);
                                                    ^                   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/usr/lib/llvm-11/include/clang/AST/Attrs.inc:887:3: note: candidate constructor not viable: requires 3 arguments, but 4 were provided
  AnnotateAttr(ASTContext &Ctx, const AttributeCommonInfo &CommonInfo
  ^
/usr/lib/llvm-11/include/clang/AST/Attrs.inc:867:7: note: candidate constructor (the implicit copy constructor) not viable: requires 1 argument, but 4 were provided
class AnnotateAttr : public InheritableParamAttr {
      ^
/usr/lib/llvm-11/include/clang/AST/Attrs.inc:867:7: note: candidate constructor (the implicit move constructor) not viable: requires 1 argument, but 4 were provided
/home/hakon/test/smokegen/astvisitor.cpp:591:53: error: no matching constructor for initialization of 'clang::AnnotateAttr'
                                    auto annotate = clang::AnnotateAttr(clang::SourceRange(), *ctx, llvm::StringRef("qt_property"), 0).clone(*ctx);
                                                    ^                   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/usr/lib/llvm-11/include/clang/AST/Attrs.inc:887:3: note: candidate constructor not viable: requires 3 arguments, but 4 were provided
  AnnotateAttr(ASTContext &Ctx, const AttributeCommonInfo &CommonInfo
  ^
/usr/lib/llvm-11/include/clang/AST/Attrs.inc:867:7: note: candidate constructor (the implicit copy constructor) not viable: requires 1 argument, but 4 were provided
class AnnotateAttr : public InheritableParamAttr {
      ^
/usr/lib/llvm-11/include/clang/AST/Attrs.inc:867:7: note: candidate constructor (the implicit move constructor) not viable: requires 1 argument, but 4 were provided
/home/hakon/test/smokegen/frontendaction.cpp:13:12: error: no template named 'make_unique' in namespace 'llvm'; did you mean 'std::make_unique'?
    return llvm::make_unique<SmokegenASTConsumer>(CI);
           ^~~~~~~~~~~~~~~~~
           std::make_unique
/bin/../lib/gcc/x86_64-linux-gnu/11/../../../../include/c++/11/bits/unique_ptr.h:961:5: note: 'std::make_unique' declared here
    make_unique(_Args&&... __args)
    ^
/home/hakon/test/smokegen/frontendaction.cpp:13:12: error: no template named 'make_unique' in namespace 'llvm'; did you mean 'std::make_unique'?
    return llvm::make_unique<SmokegenASTConsumer>(CI);
           ^~~~~~~~~~~~~~~~~
           std::make_unique
/bin/../lib/gcc/x86_64-linux-gnu/11/../../../../include/c++/11/bits/unique_ptr.h:961:5: note: 'std::make_unique' declared here
    make_unique(_Args&&... __args)
    ^
/home/hakon/test/smokegen/main.cpp:248:40: error: no matching constructor for initialization of 'clang::tooling::ToolInvocation'
        clang::tooling::ToolInvocation inv(Argv, new SmokegenFrontendAction, &FM);
                                       ^   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
/usr/lib/llvm-11/include/clang/Tooling/Tooling.h:245:3: note: candidate constructor not viable: no known conversion from 'SmokegenFrontendAction *' to 'std::unique_ptr<FrontendAction>' for 2nd argument
  ToolInvocation(std::vector<std::string> CommandLine,
  ^
/usr/lib/llvm-11/include/clang/Tooling/Tooling.h:257:3: note: candidate constructor not viable: requires 4 arguments, but 3 were provided
  ToolInvocation(std::vector<std::string> CommandLine, ToolAction *Action,
  ^
/usr/lib/llvm-11/include/clang/Tooling/Tooling.h:232:7: note: candidate constructor (the implicit copy constructor) not viable: requires 1 argument, but 3 were provided
class ToolInvocation {
      ^
2 errors generated.
make[2]: *** [CMakeFiles/smokegen.dir/build.make:95: CMakeFiles/smokegen.dir/astvisitor.cpp.o] Error 1
2 errors generated.
make[2]: *** [CMakeFiles/smokegen.dir/build.make:108: CMakeFiles/smokegen.dir/frontendaction.cpp.o] Error 1
1 error generated.
make[2]: *** [CMakeFiles/smokegen.dir/build.make:134: CMakeFiles/smokegen.dir/main.cpp.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:295: CMakeFiles/smokegen.dir/all] Error 2
make: *** [Makefile:149: all] Error 2
```
