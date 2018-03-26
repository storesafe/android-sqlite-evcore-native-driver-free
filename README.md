# Android-sqlite-evcore(-ext)-native-driver-free build (with evcore-ext user defined functions)

Provides a native build of sqlite with a low-level API for Cordova sqlite enterprise versions.

Based on [liteglue / Android-sqlite-native-driver](https://github.com/liteglue/Android-sqlite-native-driver).

by Christopher J. Brody aka Chris Brody mailto: <brodybits@litehelpers.net>

License: GPL v3 (<http://www.gnu.org/licenses/gpl.txt>) or commercial license options

## About

Android-sqlite-evcore-native-driver-free provides:
- single `EVCoreNativeDriver` class with native Java interface to the needed C functions
- automatic build for major Android targets (`armeabi`, `armeabi-v7a`, `x86`, `x86_64`, `arm64-v8a`) that is accessible from the native Java interface, with the following user defined functions:
  - `REGEXP` integrated from [brodybits / sqlite3-regexp-cached](https://github.com/brodybits/sqlite3-regexp-cached) (based on <http://git.altlinux.org/people/at/packages/?p=sqlite3-pcre.git> by Alexey Tourbin, public domain)
  - `BASE64` integrated from [brodybits / sqlite3-base64](https://github.com/brodybits/sqlite3-base64), using [brodybits / libb64-encode](https://github.com/brodybits/libb64-encode) (based on <http://libb64.sourceforge.net/> by Chris Venter, public domain)

This is accomplished by using [GlueGen](http://jogamp.org/gluegen/www/) around the C module.

**NOTE:** This project references multiple subprojects, which can resolved by: $ `make init` (as described below).

**WARNING:** The reference handles that are returned by the `EVCoreNativeDriver` library functions are raw C pointer values (with `0x100000000` added). If someone uses a reference handle that is not valid, or no longer valid with the `EVCoreNativeDriver` library the behavior is undefined (may crash, for example). It is NOT recommended to use this API directly unless you really understand how this library works internally.

## SQLite build information

### SQLite version

`3.15.2`

### SQLite build flags:

General:

- `-DSQLITE_TEMP_STORE=2`
- `-DSQLITE_THREADSAFE=2`
- `-DSQLITE_ENABLE_FTS3`
- `-DSQLITE_ENABLE_FTS3_PARENTHESIS`
- `-DSQLITE_ENABLE_FTS4`
- `-DSQLITE_ENABLE_RTREE`
- `-DSQLITE_ENABLE_FTS5`
- `-DSQLITE_ENABLE_JSON1`

Explicit default page/cache sizes (newer default values) as described at <http://sqlite.org/pgszchng2016.html>:

- `-DSQLITE_DEFAULT_PAGE_SIZE=4096`
- `-DSQLITE_DEFAULT_CACHE_SIZE=-2000`

## Dependencies

- SQLite (<https://sqlite.org/>) - public domain
- [brodybits / sqlite3-regexp-cached](https://github.com/brodybits/sqlite3-regexp-cached) - based on <http://git.altlinux.org/people/at/packages/?p=sqlite3-pcre.git> by Alexey Tourbin, public domain
- [brodybits / sqlite3-base64](https://github.com/brodybits/sqlite3-base64) - Unlicense (public domain) ref: <http://unlicense.org/>
- [brodybits / libb64-encode](https://github.com/brodybits/libb64-encode) - based on <http://libb64.sourceforge.net/> by Chris Venter, public domain

## For future consideration

- Support direct query of BLOB type

# Building

## Normal build

Initialize with the subproject references:

$ `make init`

Then to build:

$ `make`

## Regenerage Java & C glue code

$ `make regen`
