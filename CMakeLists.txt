cmake_minimum_required(VERSION 3.0.0)

message(STATUS "source path: ${PROJECT_SOURCE_DIR}")
file(GLOB PROTO_FILE proto/*.proto)
if(NOT WIN32)
    message("if NOT WIN32")

    find_package(Protobuf REQUIRED)
    PROTOBUF_GENERATE_CPP(PROTO_SRCS PROTO_HDRS ${PROTO_FILE})
else(NOT WIN32)
    message("else NOT WIN32 ${PROTO_FILE}---------------")
    foreach(proto ${PROTO_FILE})
        execute_process(
            COMMAND protoc --cpp_out=./ --proto_path=${CMAKE_CURRENT_SOURCE_DIR} ${proto}
            WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        )
    endforeach()
    # message("else NOT WIN32 ${PROTO_FILE}---------------")
    # execute_process(
    #     COMMAND cmd /c "test.bat"
    #     WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    #     RESULT_VARIABLE CMD_RESULT
    # )

    # if (CMD_RESULT EQUAL 0)
    #     message("Script executed successfully.")
    # else()
    #     message("Script execution failed with error code: ${CMD_RESULT}")
    # endif()
endif()
