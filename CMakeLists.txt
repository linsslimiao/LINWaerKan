cmake_minimum_required(VERSION 3.15)

# 设置项目名称
project(WaerKan LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Set project source files
set(SRC_FILES 
    "src/main.cpp"
)

# Set project headers
set(HEADER_FILES 
    "include/main.h"
)

# 添加库目录
link_directories(${CMAKE_SOURCE_DIR}/lib/vulkanSDK_1.3.224.1_lib)

# 添加库目录
link_directories(${CMAKE_SOURCE_DIR}/lib/glfw/lib-vc2019)

# Add executable target
add_executable(${PROJECT_NAME} ${SRC_FILES} ${HEADER_FILES})

# 添加链接库
target_link_libraries(WaerKan vulkan-1)

# 添加链接库
target_link_libraries(WaerKan glfw3)

message(STATUS "Hello World")
message(STATUS ${CMAKE_SOURCE_DIR}/lib/vulkanSDK_1.3.224.1_lib)

# Set target properties
target_include_directories(${PROJECT_NAME} PRIVATE "include")

# Set Windows Desktop Wizard settings
set_property(TARGET ${PROJECT_NAME} PROPERTY WIN32_EXECUTABLE TRUE)
set_target_properties(${PROJECT_NAME} PROPERTIES LINK_FLAGS "/DYNAMICBASE:NO /FIXED /MANIFEST:NO")
set_target_properties(${PROJECT_NAME} PROPERTIES VS_CONFIGURATION_TYPE "Application")



# 设置生成的可执行文件的子系统为控制台（Windows系统默认为窗口）
if(WIN32)
    set_target_properties(${PROJECT_NAME} PROPERTIES WIN32_EXECUTABLE FALSE)
    set_target_properties(${PROJECT_NAME} PROPERTIES LINK_FLAGS "/SUBSYSTEM:CONSOLE")
endif()