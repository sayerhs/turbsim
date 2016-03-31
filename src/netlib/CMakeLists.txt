
add_library(turbsim_netlib fftpack.f BLAS2.f sdot.f sscal.f xerbla.f spptrf.f)
target_link_libraries(turbsim_netlib nwtclibs)

