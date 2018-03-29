arduino-builder(1) -- compiles Arduino sketches
========================================================================

SYNOPSIS
--------
 **arduino-builder** _mandatory-arguments_ [_options_] _sketch_

DESCRIPTION
-----------
A command line tool for compiling Arduino sketches

This tool is able to parse Arduino Hardware specifications, properly run gcc and
produce compiled sketches.

An Arduino sketch differs from a standard C program in that it misses a main
(provided by the Arduino core), function prototypes are not mandatory, and
libraries inclusion is automagic (you just have to #include them). This tool
generates function prototypes and gathers library paths, providing gcc with all
the needed -I params.


OPTIONS
-------
Every time you run this tool, it will create a 'build.options.json' file in
build path. It's used to understand if build options (such as hardware folders,
fqbn and so on) were changed when compiling the same sketch. If they changed,
the whole build path is wiped out. If they didn't change, previous compiled
files will be reused if the corresponding source files didn't change as well.
You can save this file locally and use it instead of specifying `-hardware`,
`-tools`, `-libraries`, `-fqbn`, `-pref` and `-ide-version`.

### Mandatory

 * `-hardware` _folder_:
    _folder_ containing Arduino platforms. An example is the 'hardware' folder
    shipped with the Arduino IDE, or the packages folder created by Arduino
    Boards Manager. Can be specified multiple times. If conflicting hardware
    definitions are specified, the last one wins.

 * `-tools` _folder_:
    _folder_ containing Arduino tools (gcc, avrdude...). An example is the
    'hardware/tools' folder shipped with the Arduino IDE, or the packages folder
    created by Arduino Boards Manager. Can be specified multiple times.
    
 * `-fqbn` _name_:
    Fully Qualified Board Name, e.g.: arduino:avr:uno.
    
### Optional
    
 * `-compile` | `-dump-prefs` | `-preprocess`:
    If omitted, defaults to `-compile`. `dump-prefs` will just print all build
    preferences used, `-compile` will use those preferences to run the actual
    compiler, `-preprocess` will only print preprocessed code to stdout.

 * `-libraries` _folder_:
    _folder_ containing Arduino libraries. An example is the 'libraries' folder
    shipped with the Arduino IDE. Can be specified multiple times.

 * `-build-path` _folder_:
    _folder_ where to save compiled files. If omitted, a folder will be created
    in the temporary folder specified by your OS.

 * `-prefs`=_key_=_value_:
    It allows you to override some build properties.

 * `-warnings`:
    Can be "none", "default", "more" and "all". Defaults to "none". Used to tell
    gcc which warning level to use (-W flag).

 * `-verbose`:
    Turns on verbose mode.

 * `-quiet`:
    Suppresses almost every output.

 * `-debug-level`:
    Ddefaults to "5". Used for debugging. Set it to 10 when submitting an issue.

 * `-core-api-version`:
    Defaults to "10600". The version of the Arduino IDE which is using this
    tool.

 * `-logger`:
    Can be "human", "humantags" or "machine". Defaults to "human". If
    "humantags" the messages are qualified with a prefix that indicates their
    level (info, debug, error). If "machine", messages emitted will be in a
    format which the Arduino IDE understands and that it uses for I18N.

 * `-version`:
    If specified, prints version and exits.

 * `-build-options-file` _path_:
    _path_ to a local build.options.json file, which allows you to omit
    specifying params such as `-hardware`, `-tools`, `-libraries`, `-fqbn`,
    `-pref` and `-ide-version`.

 * `-vid-pid`:
    When specified, VID/PID specific build properties are used, if boards
    supports them.


SEE ALSO
--------
**arduino**(1)

