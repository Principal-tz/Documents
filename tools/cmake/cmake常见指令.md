----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# 学习笔记
## 简要介绍
> description	: cmake 指令

> author	: tz

> date		: 2025.05.28

> version	: v1.0
## 主要内容
> 以下描述常见的cmake指令，包括设置变量、链接库以及生成配置文件等操作

**定义变量并赋值**
```cmake
set(<variable> <value>... [PARENT_SCOPE])	# 定义变量并赋值
set(SRC_FILES main.cpp)
set(USE_FEATURE ON CACHE BOOL "enable feature")
message("Sources: ${SRC_FILES}")		# ${}引用 SRC_FILES 变量
```

**添加子目录**
```cmake
add_subdirectory(<dir> [binary_dir] [EXCLUDE_FROM_ALL])
```

**包含其他文件**
```cmake
include(CMakeLists.txt)
```

**生成可执行文件**
```cmake

```

**生成库文件**
```cmake
# add_library(<name> [STATIC|SHARED|MODULE] [source1...])
add_library(my_lib STATIC lib.cpp)
```

**为目标添加头文件搜索路径**
```cmake
# target_include_directories(<target> [SYSTEM] [BEFORE] <INTERFACE|PUBLIC|PRIVATE> [dirs...])
target_include_directories(my_lib PUBLIC include/)
```

**链接库文件**
```cmake
# target_link_libraries(<target> <PRIVATE|PUBLIC|INTERFACE> [libs...])
target_link_libraries(my_app PRIVATE my_lib pthread)
```

**循环遍历列表**
```cmake
foreach(file IN LISTS SRC_FILES)
	message("File: ${file}")
endforeach()
```

**查找外部依赖包**
```cmake
# find_package(<Package> [version] [REQUIRED])
find_package(OpenCV 4.0 REQUIRED)
```

**查找库文件路径**
```cmake
# find_library(<VAR> <name> [PATHS])
find_library(MATH_LIB m)
```

**安装目标文件到指定目录**
```cmake
# install(TARGETS <targets> DESTINATION <dir>)
install(TARGETS my_app DESTINATION bin)
```

**生成配置文件**
```cmake
# configure_file(<input> <output> [@ONLY])
configure_file(config.h.in config.h)
```

**打印消息**
```cmake
# message([STATUS|WARNING|FATAL_ERROR] "text")
message(STATUS "Configuring project...")
```

## 版本历史
> v1.0 --- 2025.05.28
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
