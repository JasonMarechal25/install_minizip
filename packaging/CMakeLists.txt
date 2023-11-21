##########################
# This file contains the instructions to generate the Bar package and install it
# Installing a target requires to know its dependency and so on thus the long list below
#

include(GNUInstallDirs)
# generate and install export file
set(TARGET_LIBS #No alias
        foo
)

install(TARGETS ${TARGET_LIBS}
        EXPORT BarTargets
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        INCLUDES DESTINATION include
)

install(EXPORT BarTargets
        FILE "BarTargets.cmake"
        NAMESPACE Bar::
        DESTINATION lib/cmake/Bar
)

include(CMakePackageConfigHelpers)

# generate the version file for the config file
write_basic_package_version_file(
        "${CMAKE_CURRENT_BINARY_DIR}/BarConfigVersion.cmake"
        VERSION "${version}"
        COMPATIBILITY SameMajorVersion
)
# create config file
configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/Config.cmake.in
        "${CMAKE_CURRENT_BINARY_DIR}/BarConfig.cmake"
        INSTALL_DESTINATION cmake
)
# install config files
install(FILES
        "${CMAKE_CURRENT_BINARY_DIR}/BarConfig.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/BarConfigVersion.cmake"
        DESTINATION lib/cmake/Bar
)

# generate the export targets for the build tree
export(EXPORT BarTargets
        FILE "${CMAKE_CURRENT_BINARY_DIR}/lib/cmake/BarTargets.cmake"
        NAMESPACE Bar::
)