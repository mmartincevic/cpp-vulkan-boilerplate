
include(ExternalProject)

set(GLM_INSTALL_PREFIX ${CMAKE_BINARY_DIR}/external/glm)

ExternalProject_Add(glm_external
    GIT_REPOSITORY https://github.com/g-truc/glm.git
    GIT_TAG 0.9.9.8
    GIT_SHALLOW ON
    CONFIGURE_COMMAND ""
    BUILD_COMMAND ""
    UPDATE_COMMAND ""
    INSTALL_COMMAND ${CMAKE_COMMAND} -E copy_directory <SOURCE_DIR>/glm ${GLM_INSTALL_PREFIX}/include/glm
    BUILD_BYPRODUCTS ${GLM_INSTALL_PREFIX}/include/glm
    CMAKE_ARGS
        -DCMAKE_INSTALL_PREFIX=${GLM_INSTALL_PREFIX}
        -DCMAKE_BUILD_TYPE=Release
    CMAKE_CACHE_ARGS
        -DCMAKE_CXX_FLAGS:STRING=${CMAKE_CXX_FLAGS}
    TEST_AFTER_INSTALL OFF
    DOWNLOAD_NO_PROGRESS ON
    LOG_CONFIGURE ON
    LOG_BUILD ON
    LOG_INSTALL ON
)

# Set variables to be used in the main CMakeLists.txt
set(GLM_INCLUDE_DIR ${GLM_INSTALL_PREFIX}/include PARENT_SCOPE)
