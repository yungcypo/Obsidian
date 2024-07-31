# raylib
raylib is a [C++](./CPP.md) library used to make games  

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

# Game
Time to organize our code a bit...  
Also added `Game::HandleInput()` implementation  

```c++
#pragma once
#include "spaceship.h"

class Game {
	private:
		Spaceship spaceship;

	public:
		Game();
		~Game();
		void Draw();
		void Update();
		void HandleInput();
};
```
> *game.h*

```c++
#include "game.h"

Game::Game()
{
	Spaceship spaceship;
}

Game::~Game() {

}

void Game::Draw() {
	spaceship.Draw();
}

void Game::HandleInput() {
	if (IsKeyDown(KEY_LEFT)) {
		spaceship.MoveLeft();
	}
	else if (IsKeyDown(KEY_RIGHT)) {
		spaceship.MoveRight();
	}
}
```
> *Game.cpp*

```c++
#include <raylib.h>
#include "game.h"
#include "spaceship.h"

int main()
{
    Color grey = {29, 29, 27, 255};

    const int screenWidth = 750;
    const int screenHeight = 700;

    InitWindow(screenWidth, screenHeight, "CppInvaders");
    SetTargetFPS(60);

    Game game;

    while (WindowShouldClose() == false) {
        game.HandleInput();

        BeginDrawing();
        ClearBackground(grey);
        game.Draw();

        EndDrawing();
    }

    CloseWindow();
}
```
> *CppInvaders.cpp*

## Spaceship movement
```c++
#include "spaceship.h"

Spaceship::Spaceship()
{
	image = LoadTexture("graphics/spaceship.png");
	position.x = (GetScreenWidth() - image.width) / 2;
	position.y = GetScreenHeight() - image.height - 50;
}

Spaceship::~Spaceship() {
	UnloadTexture(image);
}

void Spaceship::Draw() {
	DrawTextureV(image, position, WHITE);
}

void Spaceship::MoveLeft() {
	position.x -= 7;

	if (position.x < 0) {
		position.x = 0;
	}	
}

void Spaceship::MoveRight() {
	position.x += 7;
	if ((position.x + image.width) >= GetScreenWidth()) {
		position.x = (GetScreenWidth() - image.width);
	}
}
```
> *Spaceship.cpp*


# Laser
Some changes might not be listed, those are usually pretty intuitive changes   
When you see `...` in code, it means that there is some unchanged code from previous chapter  

```c++
#pragma once
#include <raylib.h>

class Laser {
	private:
		Vector2 position;
		int speed;
		bool active;

	public:
		Laser(Vector2 position, int speed);
		void Update();
		void Draw();
		bool GetActive() const;
};
```
> *laser.h*

```c++
#include "laser.h"

Laser::Laser(Vector2 position, int speed)
{
	this->position = position;
	this->speed = speed;
	this->active = true;
}

void Laser::Draw() {
	if (active) {
		DrawRectangle(position.x, position.y, 4, 15, {243, 216, 63, 255});
	}
}

void Laser::Update() {
	position.y += speed;

	if (active) {
		if (position.y < 0 || position.y > GetScreenHeight()) {
			active = false;
		}
	}
}

bool Laser::GetActive() const {
	return active;
}
```
> *Laser.cpp*

```c++
Spaceship::Spaceship()
{
	...
	std::vector<Laser> lasers;
	lastFireTime = 0.0;
}

...

void Spaceship::Shoot() {
	if (GetTime() - lastFireTime >= 0.35) {
		lasers.push_back(Laser({position.x + image.width / 2 - 2, position.y}, -6));
		lastFireTime = GetTime();
	}
}
```
> *Spaceship.cpp*

```c++
void Game::Update() {
	for (auto& laser : spaceship.lasers) {
		laser.Update();
	}

	DeleteInactiveLasers();
}

void Game::Draw() {
	spaceship.Draw();

	for (auto& laser : spaceship.lasers) {
		laser.Draw();
	}
}

void Game::HandleInput() {
	...
	if (IsKeyDown(KEY_SPACE)) {
		spaceship.Shoot();
	}
}

void Game::DeleteInactiveLasers() {
	for (auto i = spaceship.lasers.begin(); i != spaceship.lasers.end();) {
		if (!i->GetActive()) {
			i = spaceship.lasers.erase(i);
		}
		else {
			++ i;
		}
	}
}
```
> *Game.cpp*


