cmake_minimum_required(VERSION 3.22)
project(MeuAutoTool LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)
FetchContent_Declare(
    preloader
    GIT_REPOSITORY https://github.com/LiteLDev/preloader-android.git
    GIT_TAG 0.2.2 
)
FetchContent_MakeAvailable(preloader)

add_library(MeuAutoTool SHARED src/main.cpp)
target_link_libraries(MeuAutoTool PRIVATE preloader log)
target_compile_options(MeuAutoTool PRIVATE -fvisibility=hidden -s)
