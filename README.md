
# Installer Package for macOS _R_ toolchain [![License](https://img.shields.io/badge/license-GPL%20%28%3E=%202%29-brightgreen.svg?style=flat)](http://www.gnu.org/licenses/gpl-2.0.html)

The repository contains the scripts used to create an installer package (.pkg)
that contains binaries used to create the CRAN official macOS _R_ binary. 
Specifically, the installer will try to download and install:

- Xcode command line tools (XCode CLI) from Apple
- `clang4` from <http://r.research.att.com/libs/>
- `gfortran` from <https://gcc.gnu.org/wiki/GFortranBinaries#MacOS-1>

For those interested, the installer can obtained
here <https://uofi.box.com/v/r-macos-rtools-pkg>. The pre-built binaries this
installer encloses can be found at <https://developer.apple.com/download/more/>,
<http://r.research.att.com/libs/>, and <https://gcc.gnu.org/wiki/GFortranBinaries#MacOS-1>. 
Unlike the [previous installer](https://github.com/coatless/r-macos-clang), 
which only installed `clang4`, this installer requires internet access
to work.

**Financial support was provided to sign the installer by 
[Professor Timothy Bates](http://www.ed.ac.uk/profile/timothy-bates) 
of the [University of Edinburgh](http://www.ed.ac.uk/).**

## How do I use the installer?

Download it from <https://uofi.box.com/v/r-macos-rtools-pkg>, 
open the installer by right clicking to bring up menu and 
selecting "Open". From here, navigate through it like a normal
 macOS installer.

**That's it.** Once installed, you can start using compiled code
in _R_ like normal with the added benefit of `OpenMP`.

If you want to see behind the curtain, continue reading...

## What does the installer do?

The macOS _R_ toolchain installer performs four actions that require
the user's password to accomplish. These actions are:

1. download and install XCode CLI
1. download and install the `clang4` pre-made binary 
   files into the `/usr/local/clang4` directory
1. download and install `gfortran`
1. establish the proper paths for `CC`, `CXX`, `CXX**`, `FLIBS`,
    and `LDFLAGS` in the  `~/.R/Makevars` file

In essence, it provides a graphical user interface installation guide,
more secure path manipulation, and a smarter handling of a pre-existing
`~/.R/Makevars` when compared to a pure bash approach.

## Verify the Installer

Thanks to the **financial support provided by [Professor Timothy Bates](http://www.ed.ac.uk/profile/timothy-bates) of
the [University of Edinburgh](http://www.ed.ac.uk/)** to join the [Apple Developer program](https://developer.apple.com/).
The installer is now signed using [developer credentials](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

As a result, the installer should have a "lock" icon in the upper right corner:

![Signed Installer Lock Icon](readme_img/lock_icon.png)

Clicking the lock icon will reveal the signed developer certificate:

![Signed Developer Certificate](readme_img/signed_certificate.png)

With this being said, the code used to generate the installer has been made publically available under an open source license (GPL >= 2). 

## Overview of Files

Below is an abridged version of the actions of each file provided.

- `scripts/postinstall`
   - Downloads and Installs Xcode CLI, `clang4`, and `gfortran`
      - Detects the appropriate `Command Line Tools` dmg installer
	    by using a [headless cli check](https://github.com/timsutton/osx-vm-templates/blob/ce8df8a7468faa7c5312444ece1b977c1b2f77a4/scripts/xcode-cli-tools.sh#L8-L14),
		downloads the installer from <https://developer.apple.com/download/more/>,
		and installs it using `softwareupdate`.
      - Downloads the `clang-4.0.0-darwin15.6-Release.tar.gz` from
       <http://r.research.att.com/libs/> and extracts it into `/` directory 
	    so that it is installed on `/usr/local/clang4`
      - Detects the appropriate gfortran binary (either 6.1 or 6.3) from
        <https://gcc.gnu.org/wiki/GFortranBinaries#MacOS-1>, 
		downloads it from <http://coudert.name/software/>, and
		installs it into `/usr/local/gfortran`
   - Create or modify the `~/.R/Makevars` file with the necessary implicit variables
     to compile.
	   - `CC`, `CXX`, `CXX**`, and `LDFLAGS` for `clang4`
	   - `FLIBS` if on macOS Sierra / High Sierra (10.12 - 10.13) to avoid
	     a headache.
   - This is run at the _end_ of the installer routine.
- `make_installer.sh`
   - Create the installer package R binary installer `.pkg`
      - Builds the package from the extracted tar using `pkgbuild` 
      - Analyzing the package using `productbuild` to create a `distribution.xml`   
	  - Inserts customizations into the `distribution.xml` (title, background, ...)
	  - Calls `productbuild` to rebuild the package.
- `distribution.xml`
   - Customization options (e.g. title, background) of installer built by analyzing a temporary .pkg
- `build_files/Rlogo.png`
   - R logo
- `build_files/LICENSE.rtf`
   - License of the Xcode CLI, LLVM installer, and gfortran
- `build_files/WELCOME_DISPLAY.rtf`
   - Text displayed on welcome screen

# License

GPL (>= 2) 
