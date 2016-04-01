
cmake_minimum_required(VERSION 2.8.12)
project(TURBSIM Fortran C)

# Set default installation directory
get_filename_component(default_install
  "${CMAKE_SOURCE_DIR}/../install" ABSOLUTE)
set(CMAKE_INSTALL_PREFIX ${default_install} CACHE string
  "Choose installation directory; default turbsim/install" FORCE)
option(BUILD_SHARED_LIBS "Enabled building shared libraries" off)

# Set default build type to be RELEASE
if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release" CACHE STRING
    "Choose the build type: Debug Release MinSizeRel" FORCE)
endif (NOT CMAKE_BUILD_TYPE)

# Check for BLAS and LAPACK libraries
#find_package(BLAS REQUIRED)
#find_package(LAPACK REQUIRED)

# Set user selectable option to turn on/off double precision
option(DOUBLE_PRECISION "If ON, use double precision for REAL" on)

# By default we set the preprocessor and position independent code
# directives
set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -cpp -fPIC")
# Set the fortran modules to be stored in a common directory
set(CMAKE_Fortran_MODULE_DIRECTORY ${CMAKE_BINARY_DIR}/ftnmods )
# Add that to the include path
include_directories( ${CMAKE_Fortran_MODULE_DIRECTORY} )

# Force free-form compilation
get_filename_component(FCNAME ${CMAKE_Fortran_COMPILER} NAME)
if (FCNAME MATCHES "gfortran.*")
  set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -ffree-line-length-none")

  if (DOUBLE_PRECISION)
    set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -fdefault-real-8")
  endif(DOUBLE_PRECISION)
elseif (FCNAME MATCHES "ifort.*")
  if (DOUBLE_PRECISION)
    set(CMAKE_Fortran_FLAGS "${CMAKE_Fortran_FLAGS} -r8 -double_size 128")
  endif(DOUBLE_PRECISION)
endif (FCNAME MATCHES "gfortran.*")

add_subdirectory(NWTC_Library)
add_subdirectory(netlib)
add_subdirectory(turbsim)

include(CPack)

