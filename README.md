# archive-manager

This is a little utility similar to [atool](https://www.nongnu.org/atool/) or [patool](http://wummel.github.io/patool/), except:

  * Purely using bash and common utilities (e.g. `file`)
  * Implemented in a unix-like fashion with a number of separate, reusable utilities

```console
$ am foo.tar.xz c path/    # Create foo.tar.xz from path/
$ am foo.tar.xz x          # Extract archive
$ am foo.tar.xz l          # List archive
```

### Supported formats

  * Compression:
    - bzip2
    - gz
    - xz
    - z (compress)
  * Archives:
    - cpio
    - rar (extract only)
    - tar
    - zip

Adding more is pretty straightforward (see below).

### Why

Because I wanted such as an easier-to-maintain, mostly-dependency-free utility.  If you need it, you probably have bash .. but maybe not perl, python, node, etc.


## Usage

Commands may be specified using the long or short form.

### am e[x]tract

This will extract an archive, much like calling the appropriate utility, with one exception: archives with multiple files in the root will be extracted to a separate directory.

```console
$ am file.zip x
$
```

**File type:** This is determined using `file --mime-type`, rather than the filename.

### am [c]reate

This will create an archive from specified files.

```console
$ am file.zip c a.txt b.txt c.txt
   : (output)
$
```

**File type:** This is determined from the given input extension.

### am [l]ist

List an archive.  Unlike the specific commands, file names _only_ are extracted, so this may be more useful in scripts.

```console
$ am file.tar.bz2 l
   :
$
```

**File type:** Determined using `file --mime-type`


## Adding more support

For determining how to map files and extensions to compression types or suites (archive types), change the following:

  * `libexec/archive-manager/find-tool`
\
For adding a particular compression or suite, then create:

  * `libexec/archive-manager/comp-<TYPE>`
  * `libexec/archive-manager/suite-<TYPE>`

Copying one of the existing is likely the most expedient path to this.


## Caveats etc

This is bash, and probably not particularly great shell script, so caveat emptor.  Also, various _common_ utilities (and GNU variants) are assumed.

## License

GPL3

Copyright (C) 2021, Ryan Pavlik

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>.
