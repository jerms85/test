#include <cstdlib>
#include <ctime>
#include <iostream>
#include <string>
#include <conio.h>
#include <Windows.h>

using namespace std;

void setup();
void draw();
void input();
void logic();

const int MAX_WIDTH = 15;
const int MAX_HEIGHT = 15;
int playerX;
int playerY;
int trapX;
int trapY;
int treasureX;
int treasureY;
bool gameover = false;
bool win = false;


int main() {

	setup();
	while (!gameover && !win) {
		draw();
		input();
		logic();
	}
	if (gameover) {
		system("cls");
		cout << "You got killed! --- Try again!\n\n";
	}
	if (win) {
		system("cls");
		cout << "Congratulation!! you won!\n\n";
	}
	system("PAUSE");
}

void setup() {
	srand(unsigned(time(0)));
	playerX = 1;
	playerY = 1;
	gameover = false;
	trapX = rand() % MAX_WIDTH;
	trapY = rand() % MAX_HEIGHT;
	while (trapX == MAX_WIDTH - 1 && trapY == MAX_HEIGHT - 1) {
		trapX = rand() % MAX_WIDTH;
		trapY = rand() % MAX_HEIGHT;
	}
	treasureX = MAX_WIDTH - 1;
	treasureY = MAX_HEIGHT - 1;
}

void draw() {

	system("cls");
	for (int i = 0; i < MAX_HEIGHT; i++) {
		for (int j = 0; j < MAX_WIDTH; j++) {
			if (i == trapY && j == trapX)
				cout << " X ";
			else if (i == playerY && j == playerX)
				cout << " O ";
			else if (i == treasureX && j == treasureY)
				cout << " @ ";
			else {
				cout << " . ";
			}
		}
		cout << endl;
	}
	cout << "\n\n Controls:\n\tW = UP\nA = LEFT\tD = RIGHT\n\tS = DOWN\n\n";

}

void input() {

	if (_kbhit) {
		switch (_getch()) {
		case 'a': playerX--;
			break;
		case 'w': playerY--;
			break;
		case 'd': playerX++;
			break;
		case 's': playerY++;
			break;
		case 'A': playerX--;
			break;
		case 'W': playerY--;
			break;
		case 'D': playerX++;
			break;
		case 'S': playerY++;
			break;
		default:
			break;
		}
	}
}

void logic() {
	if (trapX == playerX && trapY == playerY)
		gameover = true;
	if (treasureX == playerX && treasureY == playerY)
		win = true;
	if (playerX < 0)
		gameover = true;
	if (playerX > MAX_WIDTH - 1)
		gameover = true;
	if (playerY < 0)
		gameover = true;
	if (playerY > MAX_HEIGHT - 1)
		gameover = true;
}
