[Learn Cpp](https://www.learncpp.com/)

## Configure VS Code
Add the extension **C/C++**.

Use GCC C++ compiler (g++) and GDB debugger from **mingw-w64**. Get the [latest version of MinGW-w64 via MSYS2](https://code.visualstudio.com/docs/cpp/config-mingw). In the installation, ensure **Run MSYS2** is checked. On the MSYS2 Terminal, run `pacman -S --needed base-devel mingw-w64-x86_64-toolchain` and accept the prompts. Add to the OS PATH your MinGW-w64 bin folder (default: `C:\msys64\mingw64\bin`).
The Following commands should now work on your default terminal:
```bat
rem GNU's compiler for C
gcc --version

rem GNU's compiler for C++
g++ --version

rem GNU's debugger
gdb --version
```

On Linux, run `sudo apt-get update` and `sudo apt-get install build-essential gdb`. Write a simple hello world program, run it without the debugging. When VS Code prompts, select `g++ build and debug active file`.

Configuration files in VS Code:
- tasks.json (compiler build settings)  
- launch.json (debugger settings)  
- c_cpp_properties.json (compiler path and IntelliSense settings)

## Headers & Precompiled Headers

Headers are the `#include` part of cpp files. It is typically used to declare the interface of a module or library. In a sense, it is similar to Python's `import`. Using **precompiled headers** is a common practice to accelerate builds. This is achieved by keeping a `#include "pch.h"` in every cpp file (or, in older version, `#include "stdafix.h"`).

## Build configuration
Also called **build target**, it determines how the IDE will build the project. Most IDE set up two different config files:
- **Debug configuration**  
Typically used when writing programs. This turns off all optimizations and includes debugging info, which makes the program larger and slower, but easy to debug. It is usually selected as the active configuration by default
- **Release configuration**  
Typically used when releasing to the public. Optimized for size and performance. Therefore, it is used to test performance.

On the 1st run, VS Code creates the **tasks.json** file. Add the corresponding line to each kind of build. Also, it is a good practice to deactivate compiler extensions to keep your cpp code compliant to any compiler. Generally the chosen standard for production is the penultimate or antipenultiname.
```JSON
// (...)
"args": [
    "-fdiagnostics-color=always",
    "-g",
    "-ggdb",             // Activate for Debugging Build
    //"-O2",             // Activate for Release Build
    //"-DNDEBUG",        // Activate for Release Build
    "-pedantic-errors",  // Disable compiler extensions to keep C++ code compliant
    "-Wall",             // Turn warning levels up to the max (Best practice)
    "-Weffc++",          // Turn warning levels up to the max (Best practice)
    "-Wextra",           // Turn warning levels up to the max (Best practice)
    "-Wconversion",      // Turn warning levels up to the max (Best practice)
    "-Wsign-conversion", // Turn warning levels up to the max (Best practice)
    "-Werror",           // Compiler handles Warnings as Errors (Best practice)
    "-std=c++23",        // Choose the standard
    "${file}",
    "-o",
    "${fileDirname}/${fileBasenameNoExtension}"
],
"group": {               // If not the default, change all to "group": "build",
    "kind": "build",
    "isDefault": true    
},
// (...)        
```
Map of code name when under development and their respective final name.
|While in progress | Finished|
|---|---|
|c++1x | C++11|
|c++1y | C++14|
|c++1z | C++17|
|c++2a | C++20|
|c++2b | C++23|