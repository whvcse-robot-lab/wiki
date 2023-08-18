# C/C++

在**多人协作**编写C/C++代码时应当遵循[LLVM的代码规范](https://llvm.org/docs/CodingStandards.html)

与其不同的，其中：

- C++版本
    * 除非另有说明，都应当编写C++2x程序

???+ danger "注意区分现代C++和传统C++"
    
    现代C++泛指C++11之后的版本， C++98 及其之前的 C++ 特性均称之为传统 C++。

    * 不要用C with Classes(CwC)的风格编写C++
  
- 黄金编译器
    * 桌面平台： clang/clang++
    * 嵌入式  ： gcc/g++ 

- 非标准扩展支持
    * 编译器扩展支持不属于C++的各种扩展，在任何时候都应当避免使用
    * 如有任何需求，应使用各种可移植性的包装器来使用非标准扩展

## 格式化工具

为了跨平台,针对C/C++的格式化工具采用clang-format和clang-tidy。

## 自动化构建系统

为了跨平台，任何时候应当优先使用CMake来管理工程, 在历史处理遗留问题时可以使用make。

???+ danger "任何时候都不准使用IDE内建构建系统"
    如果不能和IDE解耦，就不方便做项目管理

## IDE/编辑器支持

为了有良好的多平台语言支持，工程的自动化构建系统应当输出`compile_commands.json`做为编译数据库
（[Compilation database](https://clang.llvm.org/docs/JSONCompilationDatabase.html)）。

* 如果使用CMake，可以启用`CMAKE_EXPORT_COMPILE_COMMANDS`
* 如果使用make，可以用`bear`工具来输出

### LSP

优先使用clangd作为lsp，不要使用IDE/编辑器内建的语言支持

???+ danger "如果你使用VSCode"
    不要使用Microsoft C/C++ 插件，IntelliSense的效果不如clangd
