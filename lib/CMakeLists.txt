cmake_minimum_required(VERSION 3.12)

set(CMAKE_INTERPROCEDURAL_OPTIMIZATION TRUE)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}
        /usr/local/include
        /usr/local/include/hv
        TSMap)


add_library(Client
        cryptoClient.cpp
        binanceClient.cpp
        OKX_Client.cpp)

target_link_directories(Client PUBLIC
        "/usr/local/include"
        "/usr/local/include/hv"
        "TSMap")

set_property(TARGET Client PROPERTY CXX_STANDARD 20)