#set(CMAKE_AUTOMOC ON)
#set(CMAKE_AUTORCC ON)
#
#set(CMAKE_CXX_STANDARD 17)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)
#find_package(Qt6 COMPONENTS Core)
#find_package(Qt6 COMPONENTS Gui)
#find_package(Qt6 COMPONENTS Widgets)
#set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ./build)
#
#set(SEPC_INCLUDE /usr/include/pipewire-0.3)
#set(SEPC_INCLUDE2 /usr/include/spa-0.2)
#include_directories(${SEPC_INCLUDE} ${SEPC_INCLUDE2})
#
#FILE(GLOB SOURCE_FILES "source/*.cpp")
## set the header 
#FILE(GLOB HEADER_FILES "headers/*.h")
#set(PROJECT_SOURCES
#    ${HEADER_FILES}
#    ${SOURCE_FILES}
#)
#
## Define target properties for Android with Qt 6 as:
##    set_property(TARGET pipweire APPEND PROPERTY QT_ANDROID_PACKAGE_SOURCE_DIR
##                 ${CMAKE_CURRENT_SOURCE_DIR}/android)
## For more information, see https://doc.qt.io/qt-6/qt-add-executable.html#target-creation
#target_link_libraries(screenshot PUBLIC
#    Qt::Core
#    Qt::Gui
#    Qt::Widgets
#)
#
#install(TARGETS screenshot
#    RUNTIME DESTINATION "${INSTALL_EXAMPLEDIR}"
#    BUNDLE DESTINATION "${INSTALL_EXAMPLEDIR}"
#    LIBRARY DESTINATION "${INSTALL_EXAMPLEDIR}"
#)
## Generated from screenshot.pro.
#
cmake_minimum_required(VERSION 3.16)
project(waylandshot LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ./build)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

if(NOT DEFINED INSTALL_EXAMPLESDIR)
  set(INSTALL_EXAMPLESDIR "examples")
endif()

set(INSTALL_EXAMPLEDIR "${INSTALL_EXAMPLESDIR}/widgets/desktop/waylandshot")

find_package(Qt6 COMPONENTS Core)
find_package(Qt6 COMPONENTS Gui)
find_package(Qt6 COMPONENTS Widgets)
find_package(Qt6 COMPONENTS DBus)
set(SEPC_INCLUDE /usr/include/pipewire-0.3)
#FILE(GLOB SEPC_LIB "/usr/lib/pipewire-0.3/*.so")
set(SEPC_INCLUDE2 /usr/include/spa-0.2)
#set(SEPC_INCLUDE3 /usr/include/libportal)
include_directories(${SEPC_INCLUDE} ${SEPC_INCLUDE2} ${SEPC_INCLUDE3})

FILE(GLOB SOURCE_FILES "source/*.cpp")
# set the header 
FILE(GLOB HEADER_FILES "headers/*.h")
set(PROJECT_SOURCES
    ${HEADER_FILES}
    ${SOURCE_FILES}
)

#set(chat_SRCS)
#qt6_add_dbus_interface(chat_SRCS
#    org.freedesktop.portal.Screenshot.xml
#    screenshot_interface
#)
#qt6_add_dbus_adaptor(chat_SRCS
#    org.freedesktop.portal.Screenshot.xml
#    qobject.h
#    QObject
#    screenshot_adaptor
#)
qt_add_executable(waylandshot 
    ${PROJECT_SOURCES}
)

set_target_properties(waylandshot PROPERTIES
    WIN32_EXECUTABLE TRUE
    MACOSX_BUNDLE TRUE
)
target_link_libraries(waylandshot PUBLIC
    Qt::Core
    Qt::Gui
    Qt::Widgets
    Qt::DBus
    /usr/lib/libpipewire-0.3.so
)

install(TARGETS waylandshot
    RUNTIME DESTINATION "${INSTALL_EXAMPLEDIR}"
    BUNDLE DESTINATION "${INSTALL_EXAMPLEDIR}"
    LIBRARY DESTINATION "${INSTALL_EXAMPLEDIR}"
)
