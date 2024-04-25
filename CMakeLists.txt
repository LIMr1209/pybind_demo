cmake_minimum_required(VERSION 3.28)   #cmake 最低版本要求
project(pybind_demo) #定义工程名称,这里用demo作为工程名称
message(STATUS "Project Directory: ${PROJECT_SOURCE_DIR}") #打印相关消息消息，可以用来检查相关设置是否正确

set(CMAKE_BUILD_TYPE Release)   #指定编译类型 DEBUG/RELEASE
set(CMAKE_CXX_STANDARD 20)  # c++ 版本


#execute_process(COMMAND python3 -m pybind11 --includes OUTPUT_VARIABLE pybind_include)

#include_directories(/usr/include/python3.10) #添加引用的头文件目录，这里是相对目录的形式
#include_directories(/home/limr/.local/lib/python3.10/site-packages/pybind11/include) #添加引用的头文件目录，这里是相对目录的形式
#add_compile_options(-I/usr/include/python3.10 -I/home/limr/.local/lib/python3.10/site-packages/pybind11/include) #添加编译选项

#execute_process(COMMAND python3-config --extension-suffix OUTPUT_VARIABLE python_lib)

# include_directories(include)  包含目录
# add_library(MyLib STATIC library.cpp) 静态库
# add_library(MyLib SHARED library.cpp) 为动态库
# target_link_libraries(MyApp PRIVATE MyLib) 链接库
# add_subdirectory(subdir) # 包含子目录，该目录下应该也有一个 CMakeLists.txt 文件
# set(SOURCE_FILES main.cpp util.cpp) 设置一个变量。
# set( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin) 设定生成的可执行二进制文件存放的存放目录
# set( LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib) 设定生成的库文件的存放目录
# message("use_test ： ${SOURCE_FILES}") 调试手段message打印信息

include(FetchContent)
FetchContent_Declare(
        pybind11
        GIT_REPOSITORY https://github.com/pybind/pybind11.git
        GIT_TAG        v2.6.2
        GIT_SHALLOW    TRUE
)

FetchContent_MakeAvailable(pybind11)

pybind11_add_module(example example.cpp)
target_compile_features(example PUBLIC cxx_std_14)
set_target_properties(example PROPERTIES SUFFIX ".so")

