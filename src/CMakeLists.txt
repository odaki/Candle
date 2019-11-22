cmake_minimum_required(VERSION 3.13)
project(CandleProject)

add_subdirectory(candle)
#add_subdirectory(candleplugins)
#add_subdirectory(designerplugins)

if(APPLE)
    # add target "dmg" to build a distribution file. To use the target execute "make appdmg".
    add_custom_target(appdmg
        COMMAND cd candle
        COMMAND make dmg
    )
endif()
