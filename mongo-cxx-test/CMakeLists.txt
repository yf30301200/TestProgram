CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
PROJECT(MongoCxxTest)
SET(PROJECT_OUTNAME MongoCxxTest)

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")
endif()

IF (WIN32)
ELSEIF(WIN32)
add_definitions(-DBSONCXX_POLY_USE_STD_EXPERIMENTAL=1)
endif(WIN32)
add_definitions(-DBSONCXX_POLY_USE_MNMLSTC=1)

set (ThirdParty "E:/idzqj/Work/harry/IM-Server/vcpkg/installed/x64-windows")
#设置头文件路径
INCLUDE_DIRECTORIES(
        ${PROJECT_SOURCE_DIR}/../inc
		${PROJECT_SOURCE_DIR}/inc
		${ThirdParty}/include
)
# 设置库目录
link_directories(
        ${PROJECT_SOURCE_DIR}/../lib
)

MESSAGE("mongocxx include:" ${ThirdParty}/include)
MESSAGE("mongocxx lib:" ${ThirdParty}/lib)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

# 设置项目
file(GLOB_RECURSE SRC_FILES src/*.cpp)
file(GLOB_RECURSE HEAD_FILES inc/*.h)

ADD_EXECUTABLE(${PROJECT_OUTNAME} ${SRC_FILES} ${HEAD_FILES})
target_link_libraries(${PROJECT_OUTNAME} PRIVATE mongocxx bsoncxx)

install(TARGETS ${PROJECT_OUTNAME}
        RUNTIME DESTINATION bin)


MESSAGE(STATUS "${PROJECT_OUTNAME} is BINARY dir:" ${PROJECT_BINARY_DIR})
MESSAGE(STATUS "${PROJECT_OUTNAME} is SOURCE dir:" ${PROJECT_SOURCE_DIR})




