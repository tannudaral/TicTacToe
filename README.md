# TicTacToe-
Tic Tac Toe game created using C++ 

#include <iostream>
using namespace std;

char board[3][3] = {{'1', '2', '3'}, {'4', '5', '6'}, {'7', '8', '9'}};

char current_marker; //marker - X or 0
int current_player;

void drawBoard()
{
    cout<<"-------------\n";
    cout<<"| "<<board[0][0]<<" |"<<" "<<board[0][1]<<" |"<<" "<<board[0][2]<<" |\n";
    cout<<"-------------\n";
    cout<<"| "<<board[1][0]<<" |"<<" "<<board[1][1]<<" |"<<" "<<board[1][2]<<" |\n";
    cout<<"-------------\n";
    cout<<"| "<<board[2][0]<<" |"<<" "<<board[2][1]<<" |"<<" "<<board[2][2]<<" |\n";
    cout<<"-------------\n";
}

bool placemarker(int position)
{
    int row;
    if(position%3 == 0) 
        row = (position/3) - 1;
    else row = position/3;

    int column;
    if(position%3 == 0) 
        column=2;
    else column= (position % 3) - 1;

    if(board[row][column] != 'X' && board[row][column] != '0')
    {
        board[row][column] = current_marker;
        return true;
    }
    else return false;
}

int winner()
{
  for(int i=0; i<3; i++)
  {
    //rows
    if(board[i][0] == board[i][1] && board[i][1]== board[i][2])
    return current_player;

    //columns
    if(board[0][i] == board[1][i] && board[1][i]== board[2][i])
    return current_player;
  }
  if (board[0][0] == board[1][1] && board[1][1]== board[2][2])
    return current_player;
  if (board[0][2] == board[1][1] && board[1][1]== board[2][2])
    return current_player;
   return 0;
}

void swap_player_marker()
{
    if(current_marker == 'X') current_marker = '0';
    else current_marker='X';

    if(current_player == 1) current_player = 2;
    else current_player = 1; 
}

void game()
{
    cout<<"Henlo! Player 1 choose your marker: ";
    char position_p1;
    cin>>position_p1;

    current_player=1;
    current_marker = position_p1;

    int player_won;

    for(int i=0; i<9; i++)
    {
        cout<<"Player "<<current_player<<" , it's your turn. Enter your slot: ";
        int position;
        cin>>position;

        if(position<1 && position>9)
        {
            cout<<"Uh-oh! Invalid slot. Try another slot(1-9).";
            i--; //to give player another chance hehe
            continue;
        }

        if(!placemarker(position)) 
        {
            cout<<"Uh-oh! This space is already occupied. Try another slot.";
            i--; //to give player another chance hehe
            continue;
        }
        drawBoard();

        player_won=winner();

        if(player_won == 1) 
        {
            cout<<"Congratulations, Player 1 won!"; 
            break;
        }

        if(player_won == 2)
        {
            cout<<"Congratulations, Player 2 won!"; 
            break;
        }

        swap_player_marker();
    }

    if(player_won == 0) cout<<"Uh-oh. Its a tie.";
}

int main()
{
    game();
    return 0;
}
