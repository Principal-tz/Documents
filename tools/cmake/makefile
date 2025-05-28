这是cmake生成的构建文件，可用于cmake构建项目文件。
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# makefile  : test 文件
# author    : tz
# date      : 2025.05.28
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# 文档结构
# 每一个目录下都有CMakeLists.txt 配置文件
acMeter/
├── ./vscode              		# vscode 配置目录
│   └── setting.json      		# 配置json
├── build/                		# 构建目录（用户构建时自动生成）
├── cmake/                		# cmake 目录
│   └── toolchain_.cmake  		# 工具链文件
├── src/                  		# 源代码目录
│   ├── app/
│ 	│   ├── acSample/		  	# 主要功能目录
│	│	│	├── main.cpp	  	# 主文件
│   │	│	├── makefile		# 构建文件	
│   │	│	└── CMakeLists.txt  # acSample 目录 cmake 配置文件
│ 	│   └── CMakeLists.txt    	# app 目录 cmake 配置文件
│   ├── lib/			  		# 动态库/静态库
│   ├── test/			  		# 测试目录	
│   └── CMakeLists.txt    		# src 目录 cmake 配置文件
├── CMakeLists.txt         		# 主 CMake 配置文件
└── README.md              		# 简要介绍
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#############################################################
# 针对本目录中不包含子目录的 makefile (构建文件)
#############################################################
# 定义项目根目录
PRJDIR ?= $(shell cd ../../.. && pwd)
# 包含外部文件，makefile中无法解析.cmake文件，可能有错误
include $(PRJDIR)/include/*.cmake

# 定义平台库，-l表示链接库
PLAT_SO = -lplat_sys -lplat_msg
# 定义基础库
BASIC_SO = -lmsgInterface -lbasefun -l_auth_data

# 设置静态库打包工具，生成.a文件
AR = ar
# 定义链接选项
LIB = -lstdc++ -lpthread -lc -Wl,-rpath=/lib/hal_lib(设置运行时库搜索路径) -ldl -lm -L. -L$(debug_lib_path) $(PLAT_SO) $(BASIC_SO)
# 定义编译选项，C++用CXXFLAGS
CFLAG =-g -O -W -Wall -fPIC -std=c++11

# 定义清理命令，强制递归删除
RM 		= rm -rf
# 定义输出目标，生成可执行文件acSampleGW
OUT_OBJ = acSampleGW

# 收集源文件
SRC_DIR  =$(wildcard *.cpp)		# 收集所有.cpp文件
SRC_OBJS =$(patsubst %.cpp, %.o, $(SRC_DIR))	#替换为.o后缀

# 定义默认目标，先编译可执行文件，再安装
all:$(OUT_OBJ) install

#链接目标文件生成可执行文件
$(OUT_OBJ): $(SRC_OBJS)
	$(CPP) $(CFLAG) $(LIB) -o $(OUT_OBJ) $(SRC_OBJS)

# 编译源文件为目标文件
%.o:%.cpp
	$(CPP) $(CFLAG) -c $^ -o $@

# 清理规则
clean:
	$(RM) *.o
	$(RM) $(OUT_OBJ)
	$(RM) $(debug_bin_path)$(OUT_OBJ)
 
# 安装规则，将生成的可执行文件复制到目录中
install:
	cp -f $(OUT_OBJ) $(debug_bin_path)/
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#############################################################
# 针对本目录中包含子目录的 makefile (构建文件)
#############################################################
# 定义项目根目录
PRJDIR ?= $(shell cd ../.. && pwd)

# 包含外部文件，makefile中无法解析.cmake文件，可能有错误
include $(PRJDIR)/include/*.cmake

# 链接动态库，-l表示链接库，.so:动态库，.a:静态库
PLAT_SO = -lplat_sys -lplat_msg		# 平台库
BASIC_SO = -lmsgInterface -lbasefun -l_auth_data	# 基础库
SENIOR_SO = -lbusiInterface	# ...库

# 设置静态库打包工具，生成.a文件
AR = ar
# 定义链接选项
LIB = -lstdc++ -lpthread -lc -Wl,-rpath=/lib/hal_lib(设置运行时库搜索路径) -ldl -lm -L. -L$(debug_lib_path) $(PLAT_SO) $(BASIC_SO)
# 定义编译选项，C++用CXXFLAGS
CFLAG =-g -O -W -Wall -fPIC -std=c++11

# 定义清理命令，强制递归删除
RM 		= rm -rf
# 定义输出目标，生成可执行文件acSampleGW
OUT_OBJ = acSampleGW

# 收集源文件
SRC_DIR  =$(wildcard *.cpp)		# 收集所有.cpp文件
SRC_OBJS =$(patsubst %.cpp, %.o, $(SRC_DIR))	#替换为.o后缀

SERIAL_DIR = ./CSerialCom
SDK_SRCS = $(wildcard $(SERIAL_DIR)/*.cpp)
SDK_OBJS = $(patsubst %.cpp, %.o, $(SDK_SRCS))
# SDK_OBJS :=(SDK_SRCS:.cpp=.o)

# 定义默认目标，先编译可执行文件，再安装
all:$(OUT_OBJ) install

# 链接目标文件生成可执行文件
$(OUT_OBJ): $(SRC_OBJS) $(SDK_OBJS)
	$(CPP) $(CFLAG) $(LIB) -o $(OUT_OBJ) $(SRC_OBJS) $(SDK_OBJS)

# 编译源文件为目标文件
%.o:%.cpp
	$(CPP) $(CFLAG) -c $^ -o $@

$(SERIAL_DIR)/%.o:$(SERIAL_DIR)/%.cpp
	$(CPP) $(CFLAG) -c $^ -o $@

# 清除规则
clean:
	$(RM) *.o
	$(RM) $(SERIAL_DIR)/*.o
	$(RM) $(OUT_OBJ)
	$(RM) $(acMeter_path)/bin/*
	$(RM) $(acMeter_path)

# 安装规则
install:
	mkdir -p $(acMeter_path)/bin/		# 创建目录
	cp -f $(OUT_OBJ) jc_appcfg.json startup_app.sh $(acMeter_path)/bin/		# 复制
	chmod 777 $(acMeter_path)/bin/*.sh	# 设置脚本可执行权限（所有用户可读、可写、可执行）
	chmod 666 $(acMeter_path)/bin/*.json	# 设置配置文件读写权限（所用用户可读、可写，不可执行）
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
