cmake_minimum_required(VERSION 3.5)

project(Wuerfel_mobile VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_AUTORCC_OPTIONS "--no-compress")

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check http://doc.qt.io/qt-5/deployment-android.html for more information.
# They need to be set before the find_package(Qt5 ...) call.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()

find_package(Qt5 COMPONENTS Widgets LinguistTools REQUIRED)

set(TS_FILES Wuerfel_mobile_ja_JP.ts)

if(ANDROID)
  add_library(Wuerfel_mobile SHARED
    main.cpp
    mainwindow.cpp
    mainwindow.hpp
    mainwindow.ui
    main_resources.qrc
    ${TS_FILES}
  )
else()
  add_executable(Wuerfel_mobile
    main.cpp
    mainwindow.cpp
    mainwindow.hpp
    mainwindow.ui
    main_resources.qrc
    ${TS_FILES}
  )
endif()

target_link_libraries(Wuerfel_mobile PRIVATE Qt5::Widgets)
set_target_properties(Wuerfel_mobile PROPERTIES
    QT_ANDROID_PACKAGE_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/android
)

qt5_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})
