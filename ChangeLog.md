# ChangeLog

* __v3.2.1__ - 2019-12-17

- Provide a _C++14_ specific `SHLIB_CXX14LDFLAGS` to address issues arising with _Stan_.

* __v3.2.0__ - 2019-12-03

- Fix issue where either `~/.R/Makevars` or `~/.Renviron` were owned by `root` instead of the user. (reported in #28 by @Ptterz!)
- Change `README.md` and package installer splash screen to be explicit with what happens to pre-existing `~/.R/Makevars` and `~/.Renviron`. (reported in #27 by @joranE)

* __v3.1.0__ - 2019-11-13

- Add `CXXFLAGS` in `~/.R/Makevars` for better support prior to R 3.6.1
- Add `SHLIB_CXXLDFLAGS` in `~/.R/Makevars` to link to the R ABI
  libraries instead of system. (h/t Sebastian from the [Stan Project](https://mc-stan.org)).
- Update detection scheme for headless Xcode CLI download and installation for macOS Catalina.
- Improved installer event logging.
- Update `README.md` details on components and URLs.

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
