# Smokegen command line usage

- See [KDE TechBase: Languages/Smoke](https://techbase.kde.org/Languages/Smoke)

- For convenience, the options and switches that smokegen requries are
  stored in an xml-file. Such config files for Qt-based APIs and
  KDE-based APIs are already installed with the `smokeqt` and `smokekde`
  libs (in <prefix>/share/smokegen). Give them to smokegen with the
  `-config` option, as in
```
smokegen -config /usr/share/smokegen/kde-config.xml
```
- You can extend options, like include dirs, by giving additional
  parameters on the command line. For example, you can give additional
  include dirs with the `-I` flag:
```
smokegen -config /usr/share/smokegen/kde-config.xml -I /usr/include/MyFancyApp
```
- `smokegen --help` will show a complete list of possible options.

```
$ /opt/qt/smokegen/bin/smokegen --help
Usage: smokegen [options] [-clangOptions [options]] -- <header files>
Possible command line options are:
    -I <include dir>
    -d <path to file containing #defines>
    -dm <list of macros that should be ignored>
    -g <generator to use>
    -qt enables Qt-mode (special treatment of QFlags)
    -t resolve typedefs
    -o <output dir>
    -config <config file>
    -clangOptions <flags to pass to the clang tool>
    -h shows this message
```


