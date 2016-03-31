
add_executable(turbsim TurbSim.f90 Modules.f90 FFTMod.f90 BlankModVKM.f90
  SetVersion.f90 TSsubs.f90 RANLUX.f90)
target_link_libraries(turbsim nwtclibs turbsim_netlib)

install(TARGETS turbsim
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib )
