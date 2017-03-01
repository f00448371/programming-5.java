# programming-5.java
// // This program plays the game of Tic-Tac-Toe.
import java.util.Scanner; public class TicTacToe
{  
public static Scanner sc = new Scanner(System.in); 
public static void main(String[] args) 
{ 
final int SIZE = 4;    
char[][] board = new char[SIZE][SIZE]; // game board 
resetBoard(board); // initialize the board (with ' ' for all cells) 

//  welcome to the display board.     
System.out.println("===== WELCOME TO THE TIC-TAC-TOE !! =====\n");    
showBoard(board);  

// choose symbol (x or o) to play.    
System.out.print("  Pick a symbol to play, \"x\" or \"o\"? ");  
char Symbol1 = sc.next().toLowerCase().charAt(0); 
char Symbol2 = (Symbol1 == 'x') ? 'o' : 'x'; 

// Ask who wants to go first.   
System.out.println();     
System.out.print("  Do you want to go first (y/n)? ");  
char ans = sc.next().toLowerCase().charAt(0);  
int turn;  // 0 -- for Player1, 1 -- for Player2 
int remainCount = SIZE * SIZE; // empty cell count    

// FIRST MOVE.     if (ans == 'y')      
{
turn = 0; 
Player1(board, Symbol1); // Player1 puts his/her first step    
}    
else
{  
turn = 1;  
Player2(board, Symbol2); // Player2r puts its first step     
}     

// Show the board, and decrement the count of remaining cells.  
showBoard(board);     
remainCount--;     // Play the game until either one wins.  

boolean done = false; 
int winner = -1;   // 0 -- for Player1, 1 -- for Player2, -1 -- draw   
while (!done &amp;&amp; remainCount > 0)
{ 
// If there is a winner at this time, set the winner and the done flag to true.       
done = isGameWon(board, turn,Symbol1,Symbol2); // Did the turn win ? 
if (done)      
winner = turn; // the one who made the last move win the game      
else 
{
// No winner yet.  Find the next turn and play.        
turn = (turn + 1 ) % 2;  
if (turn == 0)          
Player1(board,Symbol1);   
else 
Player2(board,Symbol2);         // Show the board after one tic, and decrement the remaining count.
showBoard(board);
remainCount--; 
}
}     // Winner is found.  
Declare the winner.  
if (winner == 0)  
System.out.println("\n** YOU WON.  CONGRATULATIONS!! **");   
else if (winner == 1)
System.out.println("\n** YOU LOST..  Try next time :) !!"); 
else    
System.out.println("\n** DRAW... **");
}

public static void resetBoard(char[][] brd) 
{
for (int i = 0; i &lt; brd.length; i++)    
for (int j = 0; j &lt; brd[0].length; j++)
brd[i][j] = ' ';
}

public static void showBoard(char[][] brd) 
{
int numRow = brd.length;    
int numCol = brd[0].length;
System.out.println();     // First write the column header 
System.out.print("    ");     
for (int i = 0; i &lt; numCol; i++)   
System.out.print(i + "   ");  
System.out.print('\n');  
System.out.println(); // blank line after the header 

// The table  
for (int i = 0; i &lt; numRow; i++)
{
System.out.print(i + "  ");
for (int j = 0; j &lt; numCol; j++) 
{  
if (j != 0)   
System.out.print("|"); 
System.out.print(" " + brd[i][j] + " ");   
}
System.out.println();       
if (i != (numRow - 1)) 
{
// separator line 
System.out.print("   ");    
for (int j = 0; j &lt; numCol; j++) 
{     
if (j != 0)     
System.out.print("+");
System.out.print("---");     
}
System.out.println();
}  
}
System.out.println();
}

public static void Player1(char[][] brd, char usym)
{
System.out.print("\nEnter the row and column indices: ");
int rowIndex = sc.nextInt();
int colIndex = sc.nextInt();     
while (brd[rowIndex][colIndex] != ' ') 
{
System.out.print("\n!! The cell is already taken.\nEnter the row and column indices: "); 
rowIndex = sc.nextInt();       
colIndex = sc.nextInt();
}
brd[rowIndex][colIndex] = usym;  
}
public static void Player2(char[][] brd, char csym)
{
// Find the first empty cell and put a tic mark there.
for (int i = 0; i &lt; brd.length; i++) 
{
for (int j = 0; j &lt; brd[0].length; j++)
{
if (brd[i][j] == ' ')
{ 
// empty cell   
brd[i][j] = csym;          
return;  
}
}
}
}

public static boolean isGameWon(char[][] brd, int turn, char usym, char csym) 
{
char sym;
if (turn == 0)   
sym = usym;  
else
sym = csym;    
int i, j;
boolean win = false; 
// Check win by a column     
for (j = 0; j &lt; brd[0].length &amp;&amp; !win; j++) 
{
for (i = 0; i &lt; brd.length; i++)
{
if (brd[i][j] != sym)
break; 
}
if (i == brd.length)  
win = true;
}     
// Final return win
return win; 
}
}
