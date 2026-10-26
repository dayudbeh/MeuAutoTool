cmake_minimum_required(VERSION 3.22)
project(MeuAutoTool LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

include(FetchContent)

# Baixa o SDK do Preloader
FetchContent_Declare(
    preloader_android
    GIT_REPOSITORY https://github.com/LiteLDev/preloader-android.git
    GIT_TAG 0.2.2
    SOURCE_SUBDIR cmake/preloader-sdk
)

FetchContent_MakeAvailable(preloader_android)

# Cria a biblioteca do mod
add_library(MeuAutoTool SHARED src/main.cpp)

# Define os caminhos de include do Preloader
target_include_directories(MeuAutoTool PRIVATE 
    "${preloader_android_SOURCE_DIR}/include"
)

# Linka com o Preloader e a biblioteca de log do Android
target_link_libraries(MeuAutoTool PRIVATE preloader log)

# Flags de otimizacao e visibilidade
target_compile_options(MeuAutoTool PRIVATE -fvisibility=hidden -Oz -ffunction-sections -fdata-sections)
target_link_options(MeuAutoTool PRIVATE -Wl,--gc-sections -Wl,--strip-all)
