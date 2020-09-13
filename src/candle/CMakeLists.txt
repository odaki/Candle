cmake_minimum_required(VERSION 3.13)
project(Candle)

set(CANDLE_VERSION "1.2.9.1b.0")

# set(CMAKE_VERBOSE_MAKEFILE ON)

# instruct CMake to run moc automatically when needed
set(CMAKE_AUTOMOC ON)

# create code from a list of Qt designer ui files
set(CMAKE_AUTOUIC ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -W -msse3 -fvisibility=hidden -fvisibility-inlines-hidden")

if(APPLE)
    add_compile_definitions(Q_OS_MACOS)
    add_compile_definitions(GLES)
endif()
add_compile_definitions(sNan=65536)
add_compile_definitions(APP_VERSION="${CANDLE_VERSION}")
add_compile_definitions(QT_NO_DEBUG)

find_package(Qt5 COMPONENTS Core Widgets OpenGL SerialPort Script UiTools REQUIRED)

include_directories(${PROJECT_SOURCE_DIR})

file(GLOB SRC_FILES ${PROJECT_SOURCE_DIR}/*.cpp
                    ${PROJECT_SOURCE_DIR}/drawers/*.cpp
                    ${PROJECT_SOURCE_DIR}/parser/*.cpp
                    ${PROJECT_SOURCE_DIR}/widgets/*.cpp
                    ${PROJECT_SOURCE_DIR}/tables/*.cpp
                    )

qt5_add_resources(SHADER_RSC 
    ${PROJECT_SOURCE_DIR}/shaders.qrc
    ${PROJECT_SOURCE_DIR}/images.qrc
    ${PROJECT_SOURCE_DIR}/fonts.qrc
    )

if(APPLE)
    set(CANDLE_ICON ${PROJECT_SOURCE_DIR}/images/candle.icns)
    set_source_files_properties(${CANDLE_ICON} PROPERTIES MACOSX_PACKAGE_LOCATION "Resources")
    set(CANDLE_LICENSE ${PROJECT_SOURCE_DIR}/../../LICENSE)
    set_source_files_properties(${CANDLE_LICENSE} PROPERTIES MACOSX_PACKAGE_LOCATION "MacOS")
    set(CANDLE_INI ${PROJECT_SOURCE_DIR}/settings.ini)
    set_source_files_properties(${CANDLE_INI} PROPERTIES MACOSX_PACKAGE_LOCATION "MacOS")
    add_executable(${PROJECT_NAME} MACOSX_BUNDLE ${SRC_FILES} ${SHADER_RSC} ${CANDLE_ICON} ${CANDLE_LICENSE} ${CANDLE_INI})
    set_target_properties(${PROJECT_NAME} PROPERTIES
        MACOSX_BUNDLE true
        MACOSX_BUNDLE_INFO_PLIST "${CMAKE_CURRENT_SOURCE_DIR}/Info.plist.in"
        MACOSX_BUNDLE_INFO_STRING "${PROJECT_NAME} is a GRBL controller application with G-Code visualizer written in Qt."
        MACOSX_BUNDLE_ICON_FILE "candle"
        MACOSX_BUNDLE_GUI_IDENTIFIER "com.github.${PROJECT_NAME}"
        MACOSX_BUNDLE_LONG_VERSION_STRING "${PROJECT_NAME} ${CANDLE_VERSION}"
        MACOSX_BUNDLE_SHORT_VERSION_STRING "${CANDLE_VERSION}"
        MACOSX_BUNDLE_BUNDLE_NAME "${PROJECT_NAME}"
        MACOSX_BUNDLE_BUNDLE_VERSION "1.0"
        MACOSX_BUNDLE_COPYRIGHT "Copyright 2015-2016 Hayrullin Denis Ravilevich"
        )
    # add target "dmg" to build a distribution file. To use the target execute "make dmg".
    add_custom_target(dmg
        COMMAND macdeployqt ${PROJECT_NAME}.app
        COMMAND rm -f ${PROJECT_NAME}.${CANDLE_VERSION}.dmg
        COMMAND hdiutil create -srcfolder ${PROJECT_NAME}.app -volname ${PROJECT_NAME}.${CANDLE_VERSION} ${PROJECT_NAME}.${CANDLE_VERSION}.dmg
        DEPENDS ${PROJECT_NAME}
    )
else()
    add_executable(${PROJECT_NAME} ${SRC_FILES} ${SHADER_RSC})
endif()

target_link_libraries(${PROJECT_NAME}
    Qt5::Core
    Qt5::Widgets
    Qt5::OpenGL
    Qt5::Gui
    Qt5::SerialPort
    Qt5::Script
    Qt5::UiTools
    )
