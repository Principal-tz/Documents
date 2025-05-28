> [**简要介绍**]  **CMake** 和 **Makefile** 构建工具的对比，以及主要介绍 CMake 构建工具

## 1. CMake 构建
- CMake 是一个开源的跨平台构建系统工具，用于自动化管理项目软件的编译、测试和打包过程。
  
- Cmake 适合大型项目，可以跨平台进行构建。

- CMake 通过配置文件 CMakeLists.txt、工具链文件toolchain.cmake，生成适用于不同平台的构建文件（如makefile），从而简化项目编译和构建过程。

- 主要包括 CMakeLists.txt 和 toolchain.cmake 两个文件的撰写。

## 2. Makefile 构建
- Makefile 是GNU项目的一部分，它使用一种基于Tab键的语法来描述文件之间的依赖关系和构建规则。

- Makefile 适合单一平台上构建中小型项目， 主要适用于Unix和类Unix系统，可以直接被make工具处理，无需转换。

- 主要构建 makefile 文件。
