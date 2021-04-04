---
layout: post
title:  "为我的VS Code准备一个通用的C++多文件配置文件"
date:   2021-04-04 09:13:00 +0800
categories: dev
author:  Zee-hash
tags:  ["VS Code", "Multi C++ Files"]
---
> 准备一个通用的配置，便于今后使用，访问链接[TemplateForVSCode](https://github.com/Zee-hash/Templates/tree/master/TemplateForVSCode)  

## 目录结构
+ --bin       存放编译后的可执行文件
+ --include   存放头文件
+ --src       存放源文件

## 准备一份Makefile
在你项目的根目录底下新建一个Makefile文件，文件的内容如下，注意**文件名开头的M要大写**：
```
CXX       := g++
CXX_FLAGS := -std=c++17 -ggdb

BIN     := bin
SRC     := src
INCLUDE := include

LIBRARIES   :=
EXECUTABLE  := main


all: $(BIN)/$(EXECUTABLE)

run: clean all
	clear
	./$(BIN)/$(EXECUTABLE)

$(BIN)/$(EXECUTABLE): $(SRC)/*.cpp
	$(CXX) $(CXX_FLAGS) -I$(INCLUDE) $^ -o $@ $(LIBRARIES)

clean:
	-rm $(BIN)/*
```

添加完成之后，你的目录内看起来应该就像下面这样：

├── bin  
├── include  
├── src  
└── Makefile

这样，你在编译时仅需在终端输入make即可完成编译
```shell
$ make
```
## 与VS Code联动
事实上，直到上一步配置完成，我们已经可以很方便地用终端编译了，但我们用的是VS Code，如果仅仅是为了这样，为什么要使用VS Code呢?

所以接下来才是更好利用VS Code图形化界面的配置
### tasks.json
使用快捷键<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>B</kbd>或者是从菜单Terminal->Run Build Task...中选择。  
由于你打开C++文件时，按下快捷键时会提示使用默认的C++ build tasks。我们现在不用这个，所以把C++文件关闭之后再按下<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>B</kbd>。  
接下来，依次点击
+ No build task to run found. Configure Build task...
+ Create tasks.json from template
+ Others

完成之后默认产生配置文件tasks.json，如下：
```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "echo",
            "type": "shell",
            "command": "echo Hello"
        }
    ]
}
```
修改配置文件
```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "type": "shell",
            "command": "make",
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```
更改完成之后，构建时就可以直接在VS Code内部使用<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>B</kbd>完成之前【打开终端、执行make】的任务了。  
此外，还可以增加一个配置信息到"group"配置的后面，用来利用与VS Code内部的Problems面板实现联动，以显示一些错误信息。
```json
"problemMatcher": "$gcc"
```

### launch.json
当我们要调试程序时，在VS Code内按下<kbd>F5</kbd>或者在菜单中选择Run->Start Debugging时，编辑器将提示你选择环境，选择"C++(GDB/LLDB)"。在新生成的launch.json中，选择"Add configuration..."，选择"C/C++:(gdb) Launch"，将产生如下所示的配置文件：
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "enter program name, for example ${workspaceFolder}/a.out",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
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
修改"program"属性的内容为`${workspaceFolder}/bin/main`，注意，这里的main要和你之前Makefile文件中的程序名要一致。  
为了在每次调试前使用的是最新生成的程序，我们还需要增加一条配置。
```json
"preLaunchTask": "build"
```
这条配置告诉编译器在执行之前，会先执行我们之前配置的构建任务。