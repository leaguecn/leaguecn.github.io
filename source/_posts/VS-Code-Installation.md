---
title: Visual Studio Code在win7下安装笔记<!--VS-Code-Installation-->
date: 2019-05-19 07:31:00
tags:
- VS Code
- 编辑器
- Editor
- 微软
categories:
- 编程
---

## 前言|Preword
VS Code 全称Visual Studio Code是微软推出了一款跨平台的开放源码的代码编辑器。
没错，TA就是一款编辑器，不是所谓的编译器，请不要被Code误解，理解为Build Program。VS Code强大之处，除了开源，还加入了Git版本控制（还不清楚是啥功能，估计是Git同步）、代码补全（just like intellisense functions）、代码片段、代码重构等功能，深受欢迎。由于VS Code资源占用少，就连台湾 Emacs 布道师试用了VS Code以后，决定不推Emacs了。但是，VS Code的安装和配置是件令人头疼的事情。这几天利用空余时间安装了VS Code及C++的插件并把编译C++项目的配置文件走了一遍，终于可以编译C++源代码，故写下这篇安装笔记，以便后来者参考和自己学习的记录。

<!--More -->
VS Code 安装在Windows 7中，下面将在Windows 7介绍所有的安装、配置C++编译文件。
如果不是Windows 7的环境，不太推荐阅读，可能只有一些的帮助、启发，请谅解。

## 准备|Pre-requirement

+ 下载VS Code安装文件，[下载地址](https://code.visualstudio.com/Download)，选择win7 64/32Bit;
+ 下载MingW 64/32bit安装文件，并安装到相应的文件夹。


## 配置C++|Configure C++ build information

主要是配置3个文件，分别是：c_cpp_properties.json|tasks.json|launch.json。


### c_cpp_properties.json的配置

在该配置文件里，主要是编译器路径的配置、包括路径、c语言的标准、cpp语言的标准、intellisenseMode。包含的字段为：

+ compilerPath
+ includePath
+ cStandard
+ cpp Standard
+ intelliSenseMode

本人在该文件中的配置内容如下：

```json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "D:\\ProgramFiles2017\\mingw-w64\\x86_64-8.1.0-release-posix-seh-rt_v6-rev0\\bin\\g++.exe",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "gcc-x64"
        }
    ],
    "version": 4
}

```



### tasks.json的配置

该文件是编译是命令的配置，包括编译的标记、类型、命令、参数、所属组。配置的项目字段如下：

+ label
+ type
+ command
+ args
+ group

本人在该文件的配置内容如下：

```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build cpp program",
            "type": "shell",
            "command": "g++",
            "args": [
                "-g",
                "-o",
                "${fileBasenameNoExtension}.exe",
                "${file}"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```


### launch.json的配置
该文件，记录了调试生成文件的路径、调试程序路径等信息。包括的项目字段如下：

+ name
+ type
+ request
+ program
+ ...
+ miDebuggerPath
+ ...

```json
{
    "version": "0.2.0",
     "configurations": [
         {
             "name": "(gdb) Launch",
             "type": "cppdbg",
             "request": "launch",
             "program": "${workspaceFolder}/${fileBasenameNoExtension}.exe",
             "args": [],
             "stopAtEntry": true,
             "cwd": "${workspaceFolder}",
             "environment": [],
             "externalConsole": false,
             "MIMode": "gdb",
             "miDebuggerPath": "D:\\ProgramFiles2017\\mingw-w64\\x86_64-8.1.0-release-posix-seh-rt_v6-rev0\\bin\\gdb.exe",
             "setupCommands": [
                 {
                     "description": "Enable pretty-printing for gdb",
                     "text": "-enable-pretty-printing",
                     "ignoreFailures": true
                 }
             ]
         }
     ]
}

```
### 配置文件重点

在配置文件中，为了可以重复在多个源文件或者项目中使用，应该采取以下的原则：

+ 将配置文件拷贝至VS Code所有工程的根目录下；
+ 配置文件中的绝对路劲采取相对路径或者变量的设置方式。

VS Code中新建项目的步骤如下：

+ step1. 打开VS Code软件，File->Open workspace选择或新建一个工作间文件夹vsc-prj；
+ step2. 在工作间文件夹vsc-prj下面新建一个保存3个配置文件的文件夹.vscode；
+ step3. 在文件夹.vscode下依次创建3个配置文件，内容设置参照以上笔记，可以使用快捷键Ctrl+shit+p打开插件搜索，键入#cpp#选择相应的配置任务；
+ step4. 回到工作间文件夹vsc-prj，创建文件helloworld.cpp，使用测试代码作为内容；
+ step5. 使用编译快捷键Ctrl+shit+b编译源文件，并使用F5调试编译结果。

测试代码：

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{

    vector<string> msg {"Hello", "C++", "World", "from", "VS Code!"};

    for (const string& word : msg)
    {
        cout << word << " ";
    }
    cout << endl;
}

```

## 参考|References
+ https://zh.wikipedia.org/wiki/Visual_Studio_Code
+ https://code.visualstudio.com/docs/cpp/config-mingw
+ https://code.visualstudio.com/docs/cpp/config-msvc
+ https://blog.csdn.net/bat67/article/details/76095813
