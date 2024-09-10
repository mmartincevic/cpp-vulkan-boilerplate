cmake_minimum_required(VERSION 3.10)
# Set the project name
project(Playground VERSION 1.0)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Enable folder support for Visual Studio
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
# Convert tabs to spaces in Visual Studio
set(CMAKE_VS_USE_SPACES ON)
set(CMAKE_VS_INDENT_SIZE 4)

# Find all .cpp files in the src directory
file(GLOB_RECURSE SOURCES "src/*.cpp")
# Find all .h files in the include/playground directory
file(GLOB_RECURSE HEADERS "include/playground/*.h")

# Add an executable target
add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

# Add the include directory to the include path
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

# Add GLFW configuration
add_subdirectory(external/glfw)

# Add GLM configuration
add_subdirectory(external/glm)

# Add dependencies
add_dependencies(${PROJECT_NAME} GLFW_external glm_external)

# Add GLFW and GLM include directories
target_include_directories(${PROJECT_NAME} PRIVATE ${GLFW_INCLUDE_DIR} ${GLM_INCLUDE_DIR})

# Link against OpenGL and GLFW
find_package(OpenGL REQUIRED)
if(WIN32)
    target_link_libraries(${PROJECT_NAME} ${GLFW_LIB_DIR}/glfw3.lib OpenGL::GL)
else()
    target_link_libraries(${PROJECT_NAME} ${GLFW_LIB_DIR}/libglfw3.a OpenGL::GL)
endif()

# Create source groups for Visual Studio filters
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/src PREFIX "Source Files" FILES ${SOURCES})
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/include PREFIX "Header Files" FILES ${HEADERS})

# Set the startup project (optional, but helpful)
set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})

# Generate Visual Studio filters
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER "")

# Force Visual Studio to show header files in the project
set_target_properties(${PROJECT_NAME} PROPERTIES LINKER_LANGUAGE CXX)