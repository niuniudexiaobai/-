 #define _CRT_SECURE_NO_WARNINGS 1
#include"game.h"
void Initboard(char board[ROW][COL], int row, int col)
{
	int i = 0;
	int j = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
			board[i][j] = ' ';
	}
}

void Displayboard(char board[ROW][COL], int row, int col)
{
	int i;
	for (i = 0; i < row ; i++)
	{
		int j = 0;
		for(j = 0; j < col ; j++)
		{ 
			printf(" %c ", board[i][j]);
			if(j < col - 1)
				printf("|");
		}
		printf("\n");
		if (i < row - 1)
		{
			for (j = 0; j < col; j++)
			{
				printf("---");
				if (j < col - 1)
					printf("|");
			}
		}
		printf("\n");
			
	}
}

void PlayerMove(char board[ROW][COL], int row, int col)
{
	int x = 0;
	int y = 0;
	printf("玩家走->\n");
	printf("请选择坐标：\n");
	while (1)
	{
		scanf("%d.%d", &x,&y);
		if (x >= 1 && x <=row && y >= 1 && y <= col)
		{
			if (board[x - 1][y - 1] == ' ')
			{
				board[x - 1][y - 1] = '*';
				break;
			}
			else
				printf("该坐标被占用\n");
		}	
		else
			printf("坐标非法，请重新输入：\n");
	}
}
void ComputerMove(char board[ROW][COL], int row, int col)
{
	int x = 0;
	int y = 0;
	while(1)
	{
		printf("电脑走->\n");
		x = rand() % ROW;
		y = rand() % COL;
		if (board[x][y] == ' ')
		{
			board[x][y] = '#';
			break;
		}
	}
}
int IsFull(char board[ROW][COL], int row, int col)//返回1表示满，返回0表示没满
{
	int x, y;
	for (x = 0; x < row; x++)
	{
		for (y = 0; y < col; y++)
		{
			if (board[x][y] == ' ')
				return 0;
		}
	}
	return 1;
}
char Is_Winner(char board[ROW][COL], int row, int col)
{
	int i = 0;
	int j = 0;
	for (i = 0; i < ROW; i++)
	{
		if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][1]!=' ')
			return board[i][0];
	}
	for (j = 0; j < COL; j++)
	{
		if (board[0][j] == board[1][j] && board[1][j] == board[2][j] && board[1][j]!=' ')
			return board[1][j];
	}
	if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[1][1] != ' ')
	{
		return board[0][0];
	}
	if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[1][1] != ' ')
	{
		return board[1][1];
	}
	if (1 == IsFull(board, ROW, COL))
	{
		return 'Q';
	}
	return 'C';
}
