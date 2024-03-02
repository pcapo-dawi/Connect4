# Connect4
codewars 5 kyu
## Introduction
We all love to play games especially as children. I have fond memories playing Connect 4 with my brother so decided to create this Kata based on the classic game. Connect 4 is known as several names such as “Four in a Row” and “Captain’s Mistress" but was made popular by Hasbro MB Games
## Task
The game consists of a grid (7 columns and 6 rows) and two players that take turns to drop their discs. The pieces fall straight down, occupying the next available space within the column. The objective of the game is to be the first to form a horizontal, vertical, or diagonal line of four of one's own discs.

Your task is to create a Class called Connect4 that has a method called play which takes one argument for the column where the player is going to place their disc.
## Rules
If a player successfully has 4 discs horizontally, vertically or diagonally then you should return "Player n wins!” where n is the current player either 1 or 2.

If a player attempts to place a disc in a column that is full then you should return ”Column full!” and the next move must be taken by the same player.

If the game has been won by a player, any following moves should return ”Game has finished!”.

Any other move should return ”Player n has a turn” where n is the current player either 1 or 2.
 
Player 1 starts the game every time and alternates with player 2.

The columns are numbered 0-6 left to right.
## Code
````

    
public class Connect4 {
  boolean victoria = false;
  int jugador = 2;
  int[][] grid = new int[6][7];
  int columnaActual = 0;
  int filaActual = 0;
  
	public String play(int column) {
    
    // Code here
    if(victoria){
      return "Game has finished!";
    }
    jugador = jugador == 1 ? 2 : 1;
    
    for(int i = 5; i >= 0; i--){
      if(grid[i][column] == 0){
        grid[i][column] = jugador;
        columnaActual = column;
        filaActual = i;
        break;
      }
      if(grid[0][column] != 0){
        jugador = jugador == 2 ? 1 : 2;
        return "Column full!";
      }
    }
    if(Ganador(columnaActual, filaActual)){
      victoria = true;
      return "Player " + jugador + " wins!";
    }
    return "Player " + jugador + " has a turn";
  }
  private boolean Ganador(int column, int row) {
    
    if(ComprobarVertical(column) || ComprobarHorizontal(row) || ComprobarDiagonalD() || ComprobarDiagonalI()) {
      return true;
    } else {
      return false;
    }
  }
  
  private boolean ComprobarVertical(int column) {
    
    for (int i = 2; i >= 0; i--) {
      if ((grid[i][column] != 0) && (grid[i][column] == grid[i+1][column]) && (grid[i+1][column] == grid[i+2][column]) && (grid[i+2][column] == grid[i+3][column])){
        return true;
      }
    }
    
    return false;
  }
  
  private boolean ComprobarHorizontal(int row) {
    
    for (int i = 0; i <= 3; i++) {
      if ((grid[row][i] != 0) &&  (grid[row][i] == grid[row][i+1]) &&  (grid[row][i+1] == grid[row][i+2]) && (grid[row][i+2] == grid[row][i+3])){
        return true;
        }
      }
    
    return false;
  }
  
  private boolean ComprobarDiagonalD() { 
    
    for (int i = 2; i >= 0; i--) {
      for (int j = 0; j <= 3; j++) {
        if ((grid[i][j] != 0) &&  (grid[i][j] == grid[i+1][j+1]) &&  (grid[i+1][j+1] == grid[i+2][j+2]) && (grid[i+2][j+2] == grid[i+3][j+3])) {
          return true;
        }
      }
    }
    
    return false;
  }
      
  private boolean ComprobarDiagonalI() {
    
    for (int i = 5; i >= 3; i--) {
      for (int j = 0; j <= 3; j++) {
        if ((grid[i][j] != 0) &&  (grid[i][j] == grid[i-1][j+1]) && (grid[i-1][j+1] == grid[i-2][j+2]) && (grid[i-2][j+2] == grid[i-3][j+3])) {
          return true;
        }
      }
    }
    
    return false;
  }
  
}
