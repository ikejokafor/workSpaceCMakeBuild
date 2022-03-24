#####################################################################################################################################################
# CMAKE List
#
# Tips:
#   IF STATEMENT EXAMPLE:
#       set(SRCS src.cpp)
#       if(WIN32)
#           set(SRCS ${SRCS} win_src.cpp)
#       elseif(UNIX)
#           set(SRCS ${SRCS} unix_src.cpp)
#       else()
#
#       endif()
#
#   Make with Debug (Default)
#       $ cd <path_to_cmakelist.txt>
#       $ mkdir build/debug
#       $ cd build/debug
#       $ cmake ../../ -DCMAKE_BUILD_TYPE=Debug
#
#   Make with Release
#       $ cd <path_to_cmakelist.txt>
#       $ mkdir build/release
#       $ cd build/release
#       $ cmake ../../ -DCMAKE_BUILD_TYPE=Release
#   
#####################################################################################################################################################


# BEGIN CMAKE Version (Required Line) ---------------------------------------------------------------------------------------------------------------
CMAKE_MINIMUM_REQUIRED (VERSION 3.3.2)
# END CMAKE Version ---------------------------------------------------------------------------------------------------------------------------------


# BEGIN Project -------------------------------------------------------------------------------------------------------------------------------------
PROJECT(IkennaWorkSpace)
# END Project ---------------------------------------------------------------------------------------------------------------------------------------


# BEGIN External CMake files ------------------------------------------------------------------------------------------------------------------------
find_program(LSB_RELEASE_EXEC lsb_release)
execute_process(COMMAND ${LSB_RELEASE_EXEC} -is
    OUTPUT_VARIABLE LSB_RELEASE_ID_SHORT
    OUTPUT_STRIP_TRAILING_WHITESPACE
)

if(${LSB_RELEASE_ID_SHORT} STREQUAL "CentOS") # Redhat/CentOS
    # /home/mdl/izo5011/IkennaWorkSpace/izo5011_dev_tools_redhat/x86/bin/cmake -DCMAKE_CXX_FLAGS="-DMODEL_TECH" ../
    add_compile_options("-DMODEL_TECH")
    ADD_SUBDIRECTORY(modelSimServer/	)
    ADD_SUBDIRECTORY(network/	    	)
    ADD_SUBDIRECTORY(syscNetProto/	    )
    ADD_SUBDIRECTORY(SYSC_FPGA_shim/	)
    ADD_SUBDIRECTORY(fixedPoint/	    )
    ADD_SUBDIRECTORY(espresso/	    	)
    ADD_SUBDIRECTORY(espressoTester/    )
ELSE() # Ubuntu
    ADD_SUBDIRECTORY(cnn_layer_accel/model/	)
    ADD_SUBDIRECTORY(modelSimServer/	)
    ADD_SUBDIRECTORY(network/	    	)
    ADD_SUBDIRECTORY(syscNetProto/	    )
    ADD_SUBDIRECTORY(SYSC_FPGA_shim/	)
    ADD_SUBDIRECTORY(SYSC_FPGA/	    	)
    ADD_SUBDIRECTORY(fixedPoint/	    )
    ADD_SUBDIRECTORY(espresso/	    	)
    ADD_SUBDIRECTORY(espressoTester/    )
    ADD_SUBDIRECTORY(caffeDataParser/   )
ENDIF()
# END External CMake files --------------------------------------------------------------------------------------------------------------------------

