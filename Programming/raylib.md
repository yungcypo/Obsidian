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
I will create [CppInvaders](https://github.com/yungcypo/CppInvaders) as example of working in raylib

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
> *CppInvaders.cpp*  

# Spaceship  
```c++
#pragma once
#include <raylib.h>

class Spaceship {
	private:
		Texture2D image;
		Vector2 position;

	public:
		Spaceship();
		~Spaceship();
		void Draw();
		void MoveLeft();
		void MoveRight();
		void Shoot();
};
```
> *spaceship.h*  

```c++
#include "spaceship.h"

Spaceship::Spaceship()
{
	image = LoadTexture("../graphics/spaceship.png");
	position.x = (GetScreenWidth() - image.width) / 2;
	position.y = GetScreenHeight() - image.height - 50;
}

Spaceship::~Spaceship() {
	UnloadTexture(image);
}

void Spaceship::Draw() {
	DrawTextureV(image, position, WHITE);
}

```
> *Spaceship.cpp*  

In *CppInvaders* initialize new spaceship with `Spaceship spaceship;` and draw it inside while loop with `spaceship.Draw();`   

