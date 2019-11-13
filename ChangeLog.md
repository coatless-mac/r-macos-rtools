# ChangeLog

* __next version__ - XXXX-XX-XX

- TBA
* __v3.0.0__ - 2019-09-13

- Use `~/.Renviron` to setup a `PATH` variable to `clang7` compiler location.
- Deploy `*FLAGS` in `~/.R/Makevars` to successfully handle the Xcode CLI changeover
- Depend on the CRAN variants for installer packages
- Add in a statement to reset the Xcode CLI environment.

* __1.1.0__ - 2018-06-06

- Added md5 hash check to verify downloaded contents (#8)
- Changed download links to point to projects GitHub Release Page (#1)

* __1.0.0__ - 2018-03-23

- Signed GUI Installer for OS X El Capitan 10.11 - macOS High Sierra 10.13 that establishes the compilation toolchain for _R_.
- Detects, downloads, and installs the appropriate Xcode CLI and gfortran installers for supported macOS systems.
- Downloads and installs the `clang4` CRAN binary.
- Sets the proper paths for `CC`, `CXX`, `CXX**`, `FLIBS`, and `LDFLAGS` in the `~/.R/Makevars file`.
- **Financial support was provided to sign the installer by [Professor Timothy Bates](http://www.ed.ac.uk/profile/timothy-bates) of the [University of Edinburgh](http://www.ed.ac.uk/).**
