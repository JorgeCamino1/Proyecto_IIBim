# Proyecto_IIBim
Proyecto de Segundo Bimestre - Juego en c++


#include<iostream>
#include<windows.h>
#include<dos.h>
#include<conio.h>
#include<stdio.h>
#include<fstream>
using namespace std;

int puzzle[][3] = {55, 53, 50,
                   52, 54, 49,
                   56, 51};

void win(int m[][3], string playerName);
int getkey();
int check(int m[][3], int move);
int swap(int m[][3], int move, int loc);
void printBoard(int m[][3]);
void showScores();

int main()
{
    int choice;
    do {
        cout << "Menu:\n";
        cout << "1. Iniciar juego\n";
        cout << "2. Mostrar puntajes\n";
        cout << "3. Creditos\n";
        cout << "4. Salir\n";
        cout << "Ingrese su eleccion: ";
        cin >> choice;

        switch (choice) {
            case 1: {
                int move_pos, temp, loc = 9;
                string playerName;

                cout << "Ingrese su nombre: ";
                cin.ignore();  // Limpiar el buffer de entrada antes de getline
                getline(cin, playerName);

                printBoard(puzzle);

                while (1)
                {
                    move_pos = getkey();
                    loc = swap(puzzle, move_pos, loc);

                    // Para salir del juego
                    if (move_pos == 27)
                    {
                        win(puzzle, playerName);
                        break;
                    }

                    printf("\n");
                    system("cls");
                    printBoard(puzzle);
                    win(puzzle, playerName);
                }
                break;
            }
            case 2:
                showScores();
                break;
            case 3: 
                cout<<"\tCREDITOS"<<endl<<"Este juego fue realizado por Jorge Camino y Alexis Vallejo"<<endl;
                break;
            case 4:
                cout << "Saliendo del programa.\n";
                break;
            default:
                cout << "Opcion invalida. Intente de nuevo.\n";
                break;
        }
    } while (choice != 4);

    return 0;
}

int getkey()
{
    int ch;
    ch = getch();
    if (ch == 0)
    {
        ch = getch();
        return ch;
    }
    return ch;
}

int check(int m[][3], int move)
{
    // Down move
    if (move == 80)
    {
        for (int i = 0; i < 3; i++)
        {
            if (m[0][i] == 0)
                return 1;
        }
    }
    // Up move
    if (move == 72)
    {
        for (int i = 0; i < 3; i++)
        {
            if (m[2][i] == 0)
                return 1;
        }
    }
    // Right move
    if (move == 77)
    {
        for (int i = 0; i < 3; i++)
        {
            if (m[i][0] == 0)
                return 1;
        }
    }
    // Left move
    if (move == 75)
    {
        for (int i = 0; i < 3; i++)
        {
            if (m[i][2] == 0)
                return 1;
        }
    }
    return 0;
}

void printBoard(int m[][3])
{
    printf("\n\n\t Number Puzzle Game\n");
    printf("\t _________________\n");
    printf("\t|     |     |     |\n");
    printf("\t|  %c  |  %c  |  %c  |\n", m[0][0], m[0][1], m[0][2]);
    printf("\t|_____|_____|_____|\n");
    printf("\t|     |     |     |\n");
    printf("\t|  %c  |  %c  |  %c  |\n", m[1][0], m[1][1], m[1][2]);
    printf("\t|_____|_____|_____|\n");
    printf("\t|     |     |     |\n");
    printf("\t|  %c  |  %c  |  %c  |\n", m[2][0], m[2][1], m[2][2]);
    printf("\t|_____|_____|_____|\n");
}

int swap(int m[][3], int move, int loc)
{
    int temp = 0;
    if (check(m, move) == 1)
    {
        cout << "Movimiento inválido...";
        return loc;
    }
    else
    {
        if (loc == 1)
        {
            temp = m[0][0];
            if (move == 75)
            {
                m[0][0] = m[0][1];
                m[0][1] = temp;
                return 2;
            }
            if (move == 72)
            {
                m[0][0] = m[1][0];
                m[1][0] = temp;
                return 4;
            }
        }
        if (loc == 2)
        {
            temp = m[0][1];
            if (move == 77)
            {
                m[0][1] = m[0][0];
                m[0][0] = temp;
                return 1;
            }
            if (move == 72)
            {
                m[0][1] = m[1][1];
                m[1][1] = temp;
                return 5;
            }
            if (move == 75)
            {
                m[0][1] = m[0][2];
                m[0][2] = temp;
                return 3;
            }
        }
        if (loc == 3)
        {
            temp = m[0][2];
            if (move == 77)
            {
                m[0][2] = m[0][1];
                m[0][1] = temp;
                return 2;
            }
            if (move == 72)
            {
                m[0][2] = m[1][2];
                m[1][2] = temp;
                return 6;
            }
        }
        if (loc == 4)
        {
            temp = m[1][0];
            if (move == 80)
            {
                m[1][0] = m[0][0];
                m[0][0] = temp;
                return 1;
            }
            if (move == 75)
            {
                m[1][0] = m[1][1];
                m[1][1] = temp;
                return 5;
            }
            if (move == 72)
            {
                m[1][0] = m[2][0];
                m[2][0] = temp;
                return 7;
            }
        }
        if (loc == 5)
        {
            temp = m[1][1];
            if (move == 72)
            {
                m[1][1] = m[2][1];
                m[2][1] = temp;
                return 8;
            }
            if (move == 77)
            {
                m[1][1] = m[1][0];
                m[1][0] = temp;
                return 4;
            }
            if (move == 75)
            {
                m[1][1] = m[1][2];
                m[1][2] = temp;
                return 6;
            }
            if (move == 80)
            {
                m[1][1] = m[0][1];
                m[0][1] = temp;
                return 2;
            }
        }
        if (loc == 6)
        {
            temp = m[1][2];
            if (move == 72)
            {
                m[1][2] = m[2][2];
                m[2][2] = temp;
                return 9;
            }
            if (move == 77)
            {
                m[1][2] = m[1][1];
                m[1][1] = temp;
                return 5;
            }
            if (move == 80)
            {
                m[1][2] = m[0][2];
                m[0][2] = temp;
                return 3;
            }
        }
        if (loc == 7)
        {
            temp = m[2][0];
            if (move == 80)
            {
                m[2][0] = m[1][0];
                m[1][0] = temp;
                return 4;
            }
            if (move == 75)
            {
                m[2][0] = m[2][1];
                m[2][1] = temp;
                return 8;
            }
        }
        if (loc == 8)
        {
            temp = m[2][1];
            if (move == 80)
            {
                m[2][1] = m[1][1];
                m[1][1] = temp;
                return 5;
            }
            if (move == 77)
            {
                m[2][1] = m[2][0];
                m[2][0] = temp;
                return 7;
            }
            if (move == 75)
            {
                m[2][1] = m[2][2];
                m[2][2] = temp;
                return 9;
            }
        }
        if (loc == 9)
        {
            if (move == 80)
            {
                temp = m[1][2];
                m[1][2] = m[2][2];
                m[2][2] = temp;
                return 6;
            }
            if (move == 77)
            {
                temp = m[2][1];
                m[2][1] = m[2][2];
                m[2][2] = temp;
                return 8;
            }
        }
    }
    return loc;
}

void win(int m[][3], string playerName)
{
    int full = 0, k, i, j;
    if (m[0][0] == 49 && m[0][1] == 50 && m[0][2] == 51)
        full += 3;
    if (m[1][0] == 52 && m[1][1] == 53 && m[1][2] == 54)
        full += 3;
    if (m[2][0] == 55 && m[2][1] == 56)
        full += 2;

    if (full == 8)
    {
        cout << "Todos los números están en orden." << endl;

        // Abre el archivo en modo de lectura para verificar puntajes existentes
        ifstream scoreFile("puntajes.txt");
        bool jugadorExistente = false;

        if (scoreFile.is_open())
        {
            string line;
            while (getline(scoreFile, line))
            {
                // Verifica si el jugador ya tiene un puntaje registrado
                if (line.find(playerName) != string::npos)
                {
                    jugadorExistente = true;
                    break;
                }
            }
            scoreFile.close();
        }
        else
        {
            cout << "Error al abrir el archivo de puntajes." << endl;
        }

        // Abre el archivo en modo de escritura para agregar el puntaje solo si no existe
        if (!jugadorExistente)
        {
            ofstream scoreFile("puntajes.txt", ios::app);

            if (scoreFile.is_open())
            {
                scoreFile << "Jugador: " << playerName << "\t Puntaje: " << full << endl;
                scoreFile.close();
            }
            else
            {
                cout << "Error al abrir el archivo de puntajes." << endl;
            }
        }

        showScores();
    }
}

void showScores()
{
    cout << "\nPuntajes:" << endl;

    // Abre el archivo en modo de lectura
    ifstream scoreFile("puntajes.txt");

    if (scoreFile.is_open())
    {
        string line;
        while (getline(scoreFile, line))
        {
            cout << line << endl;
        }
        scoreFile.close();
    }
    else
    {
        cout << "No hay puntajes registrados." << endl;
    }
}
