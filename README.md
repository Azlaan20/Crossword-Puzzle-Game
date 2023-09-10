# 2D Crossword Puzzle Project

## Project Output

<div align="center">
    <img src="https://github.com/Azlaan20/Crossword-Puzzle-Game/blob/main/Project/Output%201.png" width="200" alt="Project Output Image 1">
    <img src="https://github.com/Azlaan20/Crossword-Puzzle-Game/blob/main/Project/Output%202.png" width="200" alt="Project Output Image 2">
    <img src="https://github.com/Azlaan20/Crossword-Puzzle-Game/blob/main/Project/Output%203.png" width="200" alt="Project Output Image 3">
    <img src="https://github.com/Azlaan20/Crossword-Puzzle-Game/blob/main/Project/Output%204.png" width="200" alt="Project Output Image 4">
    <img src="https://github.com/Azlaan20/Crossword-Puzzle-Game/blob/main/Project/Output%205.png" width="200" alt="Project Output Image 5">
</div>

## Overview

Our project is a 2D Crossword Puzzle generator and solver. It randomly generates a 9x9 crossword puzzle, and users can choose to use a previously stored character array or see a randomly generated puzzle. Users can input a word, and the program analyzes whether the input word is present in the crossword puzzle. The checking process includes examining all 8 possible directions from the starting point of the word. If the input word is found in the crossword puzzle, it is considered correct; otherwise, it's marked as incorrect. The program also provides a colour effect to highlight the correctness of the word.

## Project Details

### Department

- Department of Electrical Engineering

### Project Title

- 2D Crossword Puzzle

### Project Code

```cpp
#include<iostream>
#include<string>
#include<windows.h>
#include<fstream>
using namespace std;

int length(char name[20])
{
    int count = 0;
    char temp = 'a';
    int i = 0;
    while (temp != '\0')
    {
        temp = name[i];
        count++;
        i++;
    }
    return count;
}

bool check(char arr[9][9], char name[], int size)
{
    bool condition = false;
    int count = 0;

    //FRONT horizontal check
    for (int i = 0; i < 9; i++)
    {
        for (int j = 0; j < 9; j++)
        {
            count = 0;
            if (name[count] == arr[i][j])
            {
                while (name[count] == arr[i][j])
                {
                    if (name[count + 1] == '\0')
                    {
                        condition = true;
                        break;
                    }
                    j++;
                    count++;
                }
            }
        }
    }

    //Back horizontal check
    for (int i = 0; i < 9; i++)
    {
        for (int j = 8; j >= 0; j--)
        {
            count = 0;
            if (name[count] == arr[i][j])
            {
                while (name[count] == arr[i][j])
                {

                    if (name[count + 1] == '\0')
                    {
                        condition = true;
                        break;
                    }
                    j--;
                    count++;
                }
            }
        }
    }

    //DOWN vertical check
    for (int i = 0; i < 9; i++)
    {
        for (int j = 0; j < 9; j++)
        {
            count = 0;
            if (name[count] == arr[j][i])
            {
                while (name[count] == arr[j][i])
                {

                    if (name[count + 1] == '\0')
                    {
                        condition = true;
                        break;
                    }
                    j++;
                    count++;
                }
            }
        }
    }

    //UP vertically check
    for (int i = 8; i >= 0; i--)
    {
        for (int j = 0; j < 9; j++)
        {
            count = 0;
            if (name[count] == arr[i][j])
            {
                while (name[count] == arr[i][j])
                {

                    if (name[count + 1] == '\0')
                    {
                        condition = true;
                        break;
                    }
                    i--;
                    count++;
                }
            }
        }
    }

    //diagnol check
    for (int i = 0; i < 9; i++)
    {
        for (int j = 0; j < 9; j++)
        {
            count = 0;
            if (name[count] == arr[i][j])
            {
                while (name[count] == arr[i][j])
                {

                    if (name[count + 1] == '\0')
                    {
                        condition = true;
                        break;
                    }
                    i++;
                    j++;
                    count++;
                }
            }
        }
    }

    //Second Diagonal check
    for (int i = 8; i >= 0; i--)
    {
        for (int j = 8; j >= 0; j--)
        {
            count = 0;
            if (name[count] == arr[i][j])
            {
                while (name[count] == arr[i][j])
                {

                    if (name[count + 1] == '\0')
                    {
                        condition = true;
                        break;
                    }
                    i--;
                    j--;
                    count++;
                }
            }
        }
    }

    //Third Diagonal
    for (int i = 0; i < 9; i++)
    {
        for (int j = 0; j < 9; j++)
        {
            count = 0;
            if (name[count] == arr[i][j])
            {
                while (name[count] == arr[i][j])
                {

                    if (name[count + 1] == '\0')
                    {
                        condition = true;
                        break;
                    }
                    i++;
                    j--;
                    count++;
                }
            }
        }
    }

    //Fourth Diagonal
    for (int i = 8; i >= 0; i--)
    {
        for (int j = 8; j >= 0; j--)
        {
            count = 0;
            if (name[count] == arr[i][j])
            {
                while (name[count] == arr[i][j])
                {

                    if (name[count + 1] == '\0')
                    {
                        condition = true;
                        break;
                    }
                    i--;
                    j++;
                    count++;
                }
            }
        }
    }
    return condition;
}

void table(char b)
{
    int size;
    char name[20];
    bool condition;

    char choose;

    char grid[9][9] = { };

    anchor:
    system("cls");

    cout << "            ==============================================================" << endl << "                 > PROJECT      : 2D PUZZLE" << endl << "                 > DESIGNED BY  : AZLAAN RANJHA & RANA ABDULLAH AZHAR" << endl << "            ==============================================================" << endl << endl << endl;

    cout << "          What would you like to do?" << endl << "          1. Display Grid from File" << endl << "          2. Create a Random Grid" << endl << "          3. Exit Program" << endl << endl;

    cout << "          > Answer : ";
    cin >> choose;

    if (choose == '1')
    {
        ifstream my_file;
        string value;

        system("cls");

        my_file.open("Grid.txt");

        for (int i = 0; i < 9; i++)
        {
            for (int j = 0; j < 9; j++)
            {
                my_file >> grid[i][j];
            }
        }

        my_file.close();
    }

    else if (choose == '2') 
    {
        system("cls");

        for (int i = 0; i < 9; i++)
        {
            for (int j = 0; j < 9; j++)
            {
                b += i + j;

                if (b < 90 && b>65)
                {
                    grid[i][j] = b;
                }

                else if (b > 90)
                {
                    b = b - 25;
                    grid[i][j] = b;
                }

                else if (b < 65)
                    b = b + 25;
                grid[i][j] = b;
            }
        }
    }

    else if (choose == '3')
    {
        exit (0);
    }

    else
    {
        cout << "\n\n          " << "> INVALID INPUT! EXITING..";
        exit (0);
    }

    cout << "            ==============================================================" << endl << "                 > PROJECT      : 2D PUZZLE" << endl << "                 > DESIGNED BY  : AZLAAN RANJHA & RANA ABDULLAH AZHAR" << endl << "            ==============================================================" << endl << endl << endl;

    cout << "            * * * * * * * * * * * * * * * * * * * * * * * * *" << endl; 
    cout << "                                                               " << endl; 
    cout << "            " << grid[0][0] << "     " << grid[0][1] << "     " << grid[0][2] << "     " << grid[0][3] << "     " << grid[0][4] << "     " << grid[0][5] << "     " << grid[0][6] << "     " << grid[0][7] << "     " << grid[0][8] << endl;
    cout << "                                                               " << endl;
    cout << "                                                               " << endl;
    cout << "            " << grid[1][0] << "     " << grid[1][1] << "     " << grid[1][2] << "     " << grid[1][3] << "     " << grid[1][4] << "     " << grid[1][5] << "     " << grid[1][6] << "     " << grid[1][7] << "     " << grid[1][8] << endl;
    cout << "                                                               " << endl;
    cout << "                                                               " << endl;
    cout << "            " << grid[2][0] << "     " << grid[2][1] << "     " << grid[2][2] << "     " << grid[2][3] << "     " << grid[2][4] << "     " << grid[2][5] << "     " << grid[2][6] << "     " << grid[2][7] << "     " << grid[2][8] << endl;
    cout << "                                                               " << endl;
    cout << "                                                               " << endl;
    cout << "            " << grid[3][0] << "     " << grid[3][1] << "     " << grid[3][2] << "     " << grid[3][3] << "     " << grid[3][4] << "     " << grid[3][5] << "     " << grid[3][6] << "     " << grid[3][7] << "     " << grid[3][8] << endl;
    cout << "                                                               " << endl;
    cout << "                                                               " << endl;
    cout << "            " << grid[4][0] << "     " << grid[4][1] << "     " << grid[4][2] << "     " << grid[4][3] << "     " << grid[4][4] << "     " << grid[4][5] << "     " << grid[4][6] << "     " << grid[4][7] << "     " << grid[4][8] << endl;
    cout << "                                                               " << endl;
    cout << "                                                               " << endl;
    cout << "            " << grid[5][0] << "     " << grid[5][1] << "     " << grid[5][2] << "     " << grid[5][3] << "     " << grid[5][4] << "     " << grid[5][5] << "     " << grid[5][6] << "     " << grid[5][7] << "     " << grid[5][8] << endl;
    cout << "                                                               " << endl;
    cout << "                                                               " << endl;
    cout << "            " << grid[6][0] << "     " << grid[6][1] << "     " << grid[6][2] << "     " << grid[6][3] << "     " << grid[6][4] << "     " << grid[6][5] << "     " << grid[6][6] << "     " << grid[6][7] << "     " << grid[6][8] << endl;
    cout << "                                                               " << endl;
    cout << "                                                               " << endl;
    cout << "            " << grid[7][0] << "     " << grid[7][1] << "     " << grid[7][2] << "     " << grid[7][3] << "     " << grid[7][4] << "     " << grid[7][5] << "     " << grid[7][6] << "     " << grid[7][7] << "     " << grid[7][8] << endl;
    cout << "                                                               " << endl;
    cout << "                                                               " << endl;
    cout << "            " << grid[8][0] << "     " << grid[8][1] << "     " << grid[8][2] << "     " << grid[8][3] << "     " << grid[8][4] << "     " << grid[8][5] << "     " << grid[8][6] << "     " << grid[8][7] << "     " << grid[8][8] << endl;
    cout << "                                                               " << endl;
    cout << "            * * * * * * * * * * * * * * * * * * * * * * * * *" << endl;

    cout << "\n\n          Enter a word : ";
    cin >> name;

    size = length(name);

    condition = check(grid, name, size);

    if (condition == true)
    {
        cout << "\n          > The entered word exists in puzzle!" << endl;
        
        for (int i = 0; i < 3; i++)
        {
            system("color 20");
            system("color 07");
            system("color 20");
            system("color 07");
            system("color 20");

        }
    }

    else
    {
        for (int i = 0; i < 3; i++)
        {
            system("color 40");
            system("color 07");
            system("color 40");
            system("color 07");
            system("color 40");
        }

        cout << "\n          > The entered word does not exist in puzzle!" << endl;
    }

}

char alphabet()
{
    char alphabets[26] = { 'A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z' };

    srand(time(NULL));

    for (int i = 0; i < 9; i++)
    {
        int temp = rand() % 26;
        return alphabets[temp];
    }
}

int main()
{
    bool i = false;
    char puzzle = alphabet();

    do
    {
        puzzle += 3;
        system("cls");
        system("color 07");

        table(puzzle);                      //prints the grid on the screen

        cout << "\n          Play again?" << " [1 / 0] " << endl;
        cout << "          Your choice : ";
        cin >> i;

    } while (i);
}
```

## Usage

1. Clone the repository.
2. Compile and run the C++ code provided.
3. Follow the on-screen instructions to display a grid from a file or create a random grid.
4. Enter a word to check if it exists in the puzzle.
5. Enjoy solving crossword puzzles!

## Contributors

- Azlaan Ranjha
- Rana Abdullah Azhar
