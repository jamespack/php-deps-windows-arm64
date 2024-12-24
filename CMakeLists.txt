cmake_minimum_required(VERSION 3.18)

project(versionstest CXX)

add_executable(main main.cpp)


find_package(Iconv REQUIRED)
find_package(ZLIB REQUIRED)
find_package(LibXml2 REQUIRED)

target_link_libraries(main PRIVATE Iconv::Iconv)
target_link_libraries(main PRIVATE ZLIB::ZLIB)
target_link_libraries(main PRIVATE LibXml2::LibXml2)
