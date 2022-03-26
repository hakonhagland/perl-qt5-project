```
$ basedir=$PWD
$ cd build/qtcore
$ gdb -ex run --args /opt/qt/smokegen/bin/smokegen -p 20 \
      -config "$base_dir"/build/qtcore/config.xml \
      -smokeconfig "$base_dir"/qtcore/smokeconfig.xml \
      -L "$base_dir"/build -clangOptions -fPIC -std=c++11 \
      -- "$base_dir"/qtcore/qtcore_includes.h
[...]
Reading symbols from /opt/qt/smokegen/bin/smokegen...
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
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

Program received signal SIGILL, Illegal instruction.
Type::isAssignable (this=0x2ee0e38) at /home/hakon/test/smokegen/type.cpp:211
211	    if (klass)
(gdb) bt
#0  Type::isAssignable (this=0x2ee0e38) at /home/hakon/test/smokegen/type.cpp:211
#1  0x00007ffff48c520d in Util::addAccessorMethods (field=..., usedTypes=0x7fffffff9d60) at /home/hakon/test/smokegen/generators/smoke/helpers.cpp:811
#2  0x00007ffff48c1a59 in Util::preparse (usedTypes=0x7fffffff9d60, superClasses=0x7fffffff99d0, keys=...) at /home/hakon/test/smokegen/generators/smoke/helpers.cpp:349
#3  0x00007ffff48a9104 in SmokeDataFile::SmokeDataFile (this=0x7fffffff9d40) at /home/hakon/test/smokegen/generators/smoke/writeSmokeDataFile.cpp:53
#4  0x00007ffff4895a12 in generate () at /home/hakon/test/smokegen/generators/smoke/generator_smoke.cpp:239
#5  0x0000000000a651e3 in main (argc=14, argv=0x7fffffffb078) at /home/hakon/test/smokegen/main.cpp:287
(gdb)

```
# Backtrace links to source
- `in main(argc=14, argv=0x7fffffffb078) at /home/hakon/test/smokegen/main.cpp:287` :
  [main.cpp#L287](https://github.com/hakonhagland/smokegen/blob/hwin32/main.cpp#L287)
- `in generate() at /generators/smoke/generator_smoke.cpp:239` :
  [generators/smoke/generator_smoke.cpp:239](https://github.com/hakonhagland/smokegen/blob/hwin32/generators/smoke/generator_smoke.cpp#L239)
- `in SmokeDataFile::SmokeDataFile(this=0x7fffffff9d40) at generators/smoke/writeSmokeDataFile.cpp:53` :
  [generators/smoke/writeSmokeDataFile.cpp:53](https://github.com/hakonhagland/smokegen/blob/hwin32/generators/smoke/writeSmokeDataFile.cpp#L53)
- `in Util::preparse(usedTypes=0x7fffffff9d60, superClasses=0x7fffffff99d0, keys=...) at generators/smoke/helpers.cpp:349` : [generators/smoke/helpers.cpp:349](https://github.com/hakonhagland/smokegen/blob/hwin32/generators/smoke/helpers.cpp#L349)
- `in Util::addAccessorMethods(field=..., usedTypes=0x7fffffff9d60) at generators/smoke/helpers.cpp:811` : [generators/smoke/helpers.cpp:811](https://github.com/hakonhagland/smokegen/blob/hwin32/generators/smoke/helpers.cpp#L811)
- `in Type::isAssignable(this=0x2ee0e38) at type.cpp:211` : [type.cpp:211](https://github.com/hakonhagland/smokegen/blob/hwin32/type.cpp#L211)

# Why is `if (klass)` at [type.cpp:211](https://github.com/hakonhagland/smokegen/blob/hwin32/type.cpp#L211) an illegal instruction?

- On line 210, we have `const Class* klass = getClass();` where `getClass()` is defined at [type.h:421](https://github.com/hakonhagland/smokegen/blob/hwin32/type.h#L421):

     Class* getClass() const { return m_class; }
