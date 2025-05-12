cmake_minimum_required(VERSION 3.10)
project(PasswordManager C)

set(CMAKE_C_STANDARD 11)

# Add main.c
add_executable(password_manager main.c)

# Link OpenSSL crypto library
find_package(OpenSSL REQUIRED)
target_link_libraries(password_manager OpenSSL::Crypto)

