################################################################################
#                                                                              #
# Copyright (C) 2023 Massimo                                                                           
                                        #
# All Rights Reserved.                                                         #
#                                                                              #
################################################################################

include(CMakePackageConfigHelpers)

set(LIBRARY_TARGET_NAME utilityfunction)

set(UtilityFunctionsrc    utilityFunction.cpp
                        )

set(UtilityFunctionhdr utilityFunction.h  
                       )

add_library(${LIBRARY_TARGET_NAME} STATIC ${UtilityFunctionsrc} ${UtilityFunctionhdr})
add_library(${PROJECT_NAME}::${LIBRARY_TARGET_NAME} ALIAS ${LIBRARY_TARGET_NAME})
target_link_libraries(${LIBRARY_TARGET_NAME} PUBLIC ${Common_LIBRARIES})

target_include_directories(${LIBRARY_TARGET_NAME} PUBLIC "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
                                                         "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/${LIBRARY_TARGET_NAME}>")

install(TARGETS ${LIBRARY_TARGET_NAME}
        EXPORT ${LIBRARY_TARGET_NAME}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${LIBRARY_TARGET_NAME})
