cmake_minimum_required(VERSION 3.14)
project (llama VERSION 1.0.0)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # Produce cmpile_commands.json
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fconcepts -Wno-subobject-linkage")
set(CMAKE_BUILD_TYPE "Release")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../inc/)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../../shenango/bindings/cc/)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../../shenango/inc/)

# Link Shenango.
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../../shenango/bindings/cc/)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../../shenango/)
link_libraries(rt++ runtime net base)

# Linker script.
set(CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} -T${CMAKE_CURRENT_SOURCE_DIR}/../../shenango/base/base.ld")

# Link AIFM.
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../)
link_libraries(aifm)

# Link Pthread.
link_libraries(pthread)

# Link RDMA.
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../../shenango/rdma-core/build/lib/statics)
link_libraries(mlx5 ibverbs)

# Link netlink.
link_libraries(nl-3 nl-route-3)

# Link libnuma.
link_libraries(numa)

# link papi
link_libraries(papi)

add_executable(run_chat_far run_chat_far.cpp)