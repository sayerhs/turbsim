
# NREL TurbSim source with CMake build

This is a fork of the [NREL TurbSim](https://nwtc.nrel.gov/TurbSim) source code
to adapt it to use CMake for the build system. The source formatting has been
rearranged slightly, but otherwise no source files have been modified from the
base source downloadable at the NWTC download portal.

## Installation instructions

```
git clone <repository_url> turbsim # Clone the public repo
cd turbsim/build                   # Change into the build directory
ccmake ../src                      # Configure compilation options
make                               # Build sources 
make install                       # Install into central directory
```

## Current CMake options

* `DOUBLE_PRECISION`     - Enable double precision for REAL
* `CMAKE_BUILD_TYPE`     - RELEASE or DEBUG
* `CMAKE_INSTALL_PREFIX` - Directory where the executable is installed
* `BUILD_SHARED_LIBS`    - Enable building of shared libraries

## Other information

Please consult the official NWTC download portal for License, Disclaimer, and
documentation.
