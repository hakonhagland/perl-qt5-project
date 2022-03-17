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
smokegen --help will show a complete list of possible options.
```

