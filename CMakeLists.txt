cmake_minimum_required(VERSION 3.10)
project(PasswordManager C)

set(CMAKE_C_STANDARD 11)

add_executable(password_manager main1.c)

find_package(OpenSSL REQUIRED)
target_link_libraries(password_manager OpenSSL::Crypto)

