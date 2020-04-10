find_package(pybind11 REQUIRED)

pybind11_add_module(_utils _Demangle.cc _packaging.cc _utils.cc backtrace/_Backtrace.cc)
target_link_libraries(_utils PUBLIC utils)
install(TARGETS _utils DESTINATION ${CMAKE_INSTALL_PREFIX}/python/lsst/utils)

install(
    DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/ DESTINATION ${CMAKE_INSTALL_PREFIX}/python/lsst/utils
    PATTERN "CMakeLists.txt" EXCLUDE
    PATTERN "SConscript" EXCLUDE
    PATTERN "*.cc" EXCLUDE
)

file(GENERATE OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/version.py CONTENT "\
__version__ = 'unknown'
__all__ = ('__version__',)
")

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/version.py DESTINATION ${CMAKE_INSTALL_PREFIX}/python/lsst/utils)
