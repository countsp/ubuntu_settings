# 报错 find_package(catkin) failed. catkin was neither found in the workspace....

**原因：**

是没有从变量${CMAKE_PREFIX_PATH}中的路径搜索到.catkin

执行 echo ${CMAKE_PREFIX_PATH} 命令发现可以打印出ros路径/opt/ros/melodic。但是CMakeLists.txt指向的/opt/ros/melodic/share/catkin/cmake/toplevel.cmake打印变量${CMAKE_PREFIX_PATH}，发现输出是空的。导致cmake按照cmakelist构建时找不到${CMAKE_PREFIX_PATH}。

**解决办法：**

直接修改系统文件

1、打开toplevel.cmake文件

```
sudo gedit /opt/ros/noetic/share/catkin/cmake/toplevel.cmake
```

2、在文件/opt/ros/noetic/share/catkin/cmake/toplevel.cmake中加入

```
list(APPEND CMAKE_PREFIX_PATH "/opt/ros/melodic")
```

修改后的文件如下：

```
    # toplevel CMakeLists.txt for a catkin workspace
    # catkin/cmake/toplevel.cmake
     
    cmake_minimum_required(VERSION 3.0.2)
     
    project(Project)
     
    set(CATKIN_TOPLEVEL TRUE)
     
    #add
    list(APPEND CMAKE_PREFIX_PATH "/opt/ros/noetic")
     
    # search for catkin within the workspace
    set(_cmd "catkin_find_pkg" "catkin" "${CMAKE_SOURCE_DIR}")
    execute_process(COMMAND ${_cmd}
      RESULT_VARIABLE _res
      OUTPUT_VARIABLE _out
      ERROR_VARIABLE _err
      OUTPUT_STRIP_TRAILING_WHITESPACE
      ERROR_STRIP_TRAILING_WHITESPACE
    )
    if(NOT _res EQUAL 0 AND NOT _res EQUAL 2)
      # searching fot catkin resulted in an error
      string(REPLACE ";" " " _cmd_str "${_cmd}")
      message(FATAL_ERROR "Search for 'catkin' in workspace failed (${_cmd_str}): ${_err}")
    endif()
     
    # include catkin from workspace or via find_package()
    if(_res EQUAL 0)
      set(catkin_EXTRAS_DIR "${CMAKE_SOURCE_DIR}/${_out}/cmake")
      # include all.cmake without add_subdirectory to let it operate in same scope
      include(${catkin_EXTRAS_DIR}/all.cmake NO_POLICY_SCOPE)
      add_subdirectory("${_out}")
     
    else()
      # use either CMAKE_PREFIX_PATH explicitly passed to CMake as a command line argument
      # or CMAKE_PREFIX_PATH from the environment
      if(NOT DEFINED CMAKE_PREFIX_PATH)
        if(NOT "$ENV{CMAKE_PREFIX_PATH}" STREQUAL "")
          if(NOT WIN32)
            string(REPLACE ":" ";" CMAKE_PREFIX_PATH $ENV{CMAKE_PREFIX_PATH})
          else()
            set(CMAKE_PREFIX_PATH $ENV{CMAKE_PREFIX_PATH})
          endif()
        endif()
      endif()
     
      # list of catkin workspaces
      set(catkin_search_path "")
      foreach(path ${CMAKE_PREFIX_PATH})
        if(EXISTS "${path}/.catkin")
          list(FIND catkin_search_path ${path} _index)
          if(_index EQUAL -1)
            list(APPEND catkin_search_path ${path})
          endif()
        endif()
      endforeach()
     
      # search for catkin in all workspaces
      set(CATKIN_TOPLEVEL_FIND_PACKAGE TRUE)
      find_package(catkin QUIET
        NO_POLICY_SCOPE
        PATHS ${catkin_search_path}
        NO_DEFAULT_PATH NO_CMAKE_FIND_ROOT_PATH)
      unset(CATKIN_TOPLEVEL_FIND_PACKAGE)
     
      if(NOT catkin_FOUND)
        message(FATAL_ERROR "find_package(catkin) failed. catkin was neither found in the workspace nor in the CMAKE_PREFIX_PATH. One reason may be that no ROS setup.sh was sourced before.")
      endif()
    endif()
     
    catkin_workspace()
```
