cmake_minimum_required(VERSION 3.9)
project(b6)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake_modules/)

add_library(b6 STATIC Device.cc Device.hh Packet.cc Packet.hh Error.hh Enum.hh Device.cc Packet.cc)

# Directly set the include directory for libusb
include_directories(C:/Users/joshl/Documents/VS_projects/LiIon_charger_interface/libusb-1.0.27/include)

# Find the libusb libraries. Adjust the path as necessary to point to where the libusb libraries are located.
find_library(LIBUSB_LIBRARY
             NAMES libusb-1.0 usb-1.0
             PATHS C:/Users/joshl/Documents/VS_projects/LiIon_charger_interface/libusb-1.0.27/VS2022/MS64/dll)
if(NOT LIBUSB_LIBRARY)
    message(FATAL_ERROR "libusb library not found")
else()
    message(STATUS "libusb found: ${LIBUSB_LIBRARY}")
endif()

target_link_libraries(b6 ${LIBUSB_LIBRARY})

install(TARGETS b6 DESTINATION lib)
install(FILES Device.hh Packet.hh Error.hh Enum.hh DESTINATION include/b6)
