/*
 *
 *
 *
 *
 *
 */


import java.util.Scanner;
public class SinglePlayer{
    public static void main(String[]args){
    	Scanner input=new Scanner(System.in);
    	int x=1, y=1;
    	int pCount, aiScore=0, aiTurn=0, turnPoint=0, die1=0, die2=0, thisPoint=0, userTurn=0; //AI ints
    	int Player1S=0, Player2S=0; //Starts score off at zero points
    	int Player1RS=0, Player2RS=0; //Adds up total points in the round
    	final int FINAL=100;

    	String Turn="P1"; //Starts while game on Player 1's turn each game
    	String Roll="y"; //Starts off the player as rolling unless told otherwise
    	String test="y";
    	System.out.println("Welcome to the game of PIG!");

    		System.out.println("How many people are playing? (1 or 2)");	//Decide the number of players
    		pCount =input.nextInt();
    		if (pCount ==1){
    			while(Player1S<=FINAL||aiScore<=FINAL){

    				aiTurn =1;
    				while (aiTurn==1){ //runs the AI turn
    					die1=(int)((Math.random()*6)+1);
    					die2=(int)((Math.random()*6)+1);
    					thisPoint= die1+die2;

    				if (die1 == 1 && die2 == 1) { //if both dice rolled are 1's, erases score and trades turns.
    					System.out.println("The Computer rolled two zeros, lost its score and it is now your turn.");
    					aiScore=0;
    					userTurn=1;
    					aiTurn=2;
    				}
    				else if (die1 == 1 || die2==1){ //if either of the AI's first roll of dice is zero, it should end.
    					System.out.println("The Computer rolled one zero, it lost its points for the turn and it is now your turn to roll.");
    					aiScore = aiScore - turnPoint;
    					turnPoint=0;
    					userTurn=1;
    					aiTurn=2;
    				}
    				else {
    					aiScore=(aiScore + thisPoint);
    					System.out.println("The AI rolled a "+die1+" and a "+die2+" for a new total of "+ aiScore);
    						if (turnPoint+thisPoint>=20){
    							System.out.println("The AI ends their turn.");
    							turnPoint = turnPoint + thisPoint;
    							aiScore = aiScore + turnPoint;
    							userTurn=1;
    							aiTurn=2;
    						}
    						else if (turnPoint<20){
    							System.out.println("The AI rolls again");
    							turnPoint = turnPoint + thisPoint;
    							userTurn=1;
    						}
    				}
   	 	}

    		//RUNS UNTIL THE END OF ITS FIRST TURN
    			//user turn
    			while (userTurn==1){
    				Player1RS=0;

   				System.out.println("Player 1's total score is: "+Player1S);
   				System.out.print("Would you like to roll? [y, n]: \n");
   				input.nextLine();
    			Roll=input.nextLine();
    			System.out.println("\n----------------------------------------\n");
    			y=1;
    			while(x==y){
    				if(Roll.equalsIgnoreCase("y")){
    					die1=(int)((Math.random()*6)+1);
    					die2=(int)((Math.random()*6)+1);
    					Player1RS = Player1RS + (die1 + die2);
    					System.out.println("You rolled a "+die1+" and a "+die2+" Your round total is "+ Player1RS);
    					if(die1==1||die2==1){
    						Player1RS=0;
    						System.out.println("You rolled a zero, your score for this turn has reset and you loose your turn.");
    						if(die1==1&&die2==1){
    							System.out.println("Actually, you rolled two zeros. Your entire score has been reset.");
    							Player1S=0;
    							Player1RS=0;

    						}

    						y=0;
    					}
    					else{

    						System.out.println("Player 1's total score this round is: "+Player1RS);
    						System.out.print("Would you like to roll again and be a PIG? [y, n]: ");
    						Roll=input.nextLine();
    					}
    				}
    				else{
    					System.out.println("Player 1's turn has been skipped!");
    					y=0;
    				}
    				System.out.println("\n----------------------------------------\n");
   				}
   				Player1S=Player1S+Player1RS;
   				userTurn=0;
   				aiTurn=1;
    				}
    			}
    		}
   		}
}
//END OF AI GAME
