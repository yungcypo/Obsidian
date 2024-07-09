# raylib
raylib is a [C++](CPP.md) library used to make games  

# Install
Steps to start with raylib on Windows

## Visual Studio
Open [this link](https://visualstudio.microsoft.com/) to download Visual Studio Installer  
Install *"Visual Studio Community 2022"* with *"Desktop development witch C++"* workload  

After installing, *Create new project (Console App)*  
You can hit *F5* to run your project  

## vcpkg
vckpkg is C++ Library Manager for Windows, Linux and MacOS developed by Microsoft  

Download it from their [Github](https://github.com/microsoft/vcpkg)  
Extract downloaded file  
Open terminal in *vcpkg* folder  
Run following commands  
```shell
./bootstrap-vcpkg.bat  # prepare to use vcpkg on system
./vcpkg integrate install  # integrate Visual Studio with vcpkg
./vcpkg install raylib:x64-windows  # intall raylib
```

## Use raylib in Visual Studio
Import raylib - `#include "raylib.h"`  
Now you can use raylib in Visual Studio :)  

> Note: you might need to restart Visual Studio  

--- 

From this point, I will focus on how to work with raylib  

# First steps
Setting up a game loop and displaying blank raylib window  

```c++
#include <raylib.h>

int main()
{
    Color grey = {29, 29, 27, 255};

    const int screenWidth = 750;
    const int screenHeight = 700;

    InitWindow(screenWidth, screenHeight, "CppInvaders");
    SetTargetFPS(60);

    while (WindowShouldClose() == false) {
        BeginDrawing();
        ClearBackground(grey);

        EndDrawing();
    }
    
    CloseWindow();
}
```
