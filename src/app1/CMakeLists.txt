set(TARGET_NAME app1)
add_executable(app1 
        main.cpp
)

if(NOT "${CMAKE_CXX_STANDARD}")
  set(CMAKE_CXX_STANDARD 20)
endif()

SET(CMAKE_EXE_LINKER_FLAGS "-v")

target_include_directories(app1 
        PRIVATE 
                ${CMAKE_SOURCE_DIR} 
        PUBLIC 
                ${CMAKE_CURRENT_SOURCE_DIR}/include 
        )

if( DEFINED PLATFORM_DREAMCAST)
        #include("/opt/toolchains/dc/kos/utils/cmake/dreamcast.cmake")
        set(ROMDISK_DIR "romdisk")
        set(MKDCDISC "/opt/mkdcdisc/builddir/mkdcdisc")
        kos_add_romdisk(${TARGET_NAME} ${ROMDISK_DIR})

        # Creating cdi image after build
        # Note that it requires that a bin directory exist in project root directory
        add_custom_command(TARGET ${TARGET_NAME}
                COMMAND ${MKDCDISC} 
                -e ${CMAKE_CURRENT_BINARY_DIR}/${TARGET_NAME}.elf 
                -o ${CMAKE_SOURCE_DIR}/bin/${TARGET_NAME}.cdi 
                -n ${TARGET_NAME}  
                -v 3
                COMMENT "Making CDI image"
        )
else()
        # Copying assets to build dir
        add_custom_target(copy_assets
        COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/romdisk ${CMAKE_CURRENT_BINARY_DIR}/assets
        )
        add_custom_target(copy_assets_test
        COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/romdisk ${CMAKE_CURRENT_BINARY_DIR}/test/assets
        )
endif()

target_link_libraries(
        app1 
        PRIVATE
                dcplib
        PUBLIC
)