cmake_minimum_required(VERSION 3.28)

project(tbstack VERSION 1.0.0 LANGUAGES C)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")


add_executable(tbcstack
 src/backtrace.c
 src/mem_map.c
 src/proc.c
 src/snapshot.c
 src/tbstack.c
 src/unwind.c
)

find_package(LibDwarf REQUIRED)

find_package(PkgConfig REQUIRED)
pkg_check_modules(libelf REQUIRED IMPORTED_TARGET libelf)

find_package(PkgConfig REQUIRED)
pkg_check_modules(libunwind REQUIRED IMPORTED_TARGET libunwind)
pkg_check_modules(libunwind-ptrace REQUIRED IMPORTED_TARGET libunwind-ptrace)

target_link_libraries(tbcstack 
  PRIVATE 
    LibDwarf::LibDwarf
    PkgConfig::libelf
    PkgConfig::libunwind
    PkgConfig::libunwind-ptrace
)

target_compile_definitions(tbcstack
  PRIVATE 
    PACKAGE_STRING="${PROJECT_NAME} ${PROJECT_VERSION}"
    _GNU_SOURCE
)

