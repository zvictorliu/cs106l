---
description: Multi-File Programs, Abstraction, Preprocessor
---

模块化，只需知道如何用而不是底层细节，这就是Abstraction

三个阶段：preprocessing, compiling, linking

## preprocessing

`#include` 将对应文件的内容复制粘贴到本文件中，由于有可能重复导入，所以一般需要 *include guard*

`#define` 相当于查找替换，第一个词之后，到换行符之前的所有内容

### include guard



## compiling

检查语法错误，对于函数有声明即可通过，并不需要其实现部分

## linking

合并在一起，需要声明和实现匹配