# assignment3
import java.util.Scanner;
public class HangmanGame{
  
  public static void main(String[] args){
    Scanner reader = new Scanner(System.in); //The person choosing the word
    System.out.println("Enter a four-letter word to be guessed");
    String word = reader.next();
    
    runGame(word);
    
    
    reader.close();
  }
  
  //printHanging takes as input the number of misses the player has made,
  //and prints out the hangman corresponding to the number of misses they have made
  //printHanging does not return any values
  public static void printHanging(int misses){
    //Initially, no part of the hangman should be drawn, leave blank spaces for each
    String head = " ", body = " ", larm = " ", rarm = " ", lleg = " ", rleg = " ";
    switch (misses){
      default: head = "0"; //After making 6 or more misses, we add on the head - the player has lost
      case 5: rleg = "\\"; //After making 5 or more misses, we draw the right leg
      case 4: lleg = "/";  //After making 4 or more misses, we draw the left leg
      case 3: rarm = "\\"; //After making 3 or more misses, we draw the right arm
      case 2: larm = "/";  //After making 2 or more misses, we draw the left arm
      case 1: body = "|";  //After making 1 or more misses, we draw the body
      case 0: ;            //With 0 misses, nothing should be drawn
    }    
    //Print statement which draws the hangman
    System.out.println("___________\n" +
                       "|         |\n" +
                       "|         " + head +"\n" +
                       "|        " + larm + body + rarm + "\n" +
                       "|       " + larm + " " + body + " " + rarm + "\n" +
                       "|        " + lleg + " " + rleg + "\n" +
                       "|       " + lleg + "   " + rleg + "\n" +
                       "|__________\n");
   }
  
  
  
  //printWord prints the 4 letter word based on which letters have been correctly guessed.
  //It takes as input the String corresponding to the word being guessed,
  //as well as a boolean value for each letter in the word - representing whether or not that
  //particular letter has been guessed yet.
  public static void printWord(String word, boolean pos0, boolean pos1, boolean pos2, boolean pos3){
    //if letter at position 0 has been guessed, print the character at position 0, otherwise print _
    if(pos0){
      System.out.print(" " + word.charAt(0) + " ");
    }else{
      System.out.print(" _ ");
    }
    //if letter at position 1 has been guessed, print the character at position 1, otherwise print _
    if(pos1){
      System.out.print(" " + word.charAt(1) + " ");
    }else{
      System.out.print(" _ ");
    }
    //if letter at position 2 has been guessed, print the character at position 2, otherwise print _
    if(pos2){
      System.out.print(" " + word.charAt(2) + " ");
    }else{
      System.out.print(" _ ");
    }
    
    //if letter at position 3 has been guessed, print the character at position 3, otherwise print _
    if (pos3){
      System.out.println(" " + word.charAt(3) + " ");
    }else{
      System.out.println(" _ ");
    }   
  }
  
  //Determines if the guessed letter is in the word
  public static int isLetterInWord(String word, char a){
    if(toUpperCase(word.charAt(0))==toUpperCase(a)){
      return 0;
    }
    else if(toUpperCase(word.charAt(1))==toUpperCase(a)){
      return 1;
    }
    else if(toUpperCase(word.charAt(2))==toUpperCase(a)){
      return 2;
    }
    else if(toUpperCase(word.charAt(3))==toUpperCase(a)){
      return 3;
    }
    else{
      return -1;
    }
  }
  
  //This changes the user's letter input to uppercase if it was in lowercase form
  public static char toUpperCase (char a){
    final int UPPERCASE_CHANGE_FACTOR = 32; 
    if(a>='a' && a<='z'){
      a-=UPPERCASE_CHANGE_FACTOR;
    }
    return a;
  }
  
  //This is the game loop
  public static void runGame(String word){
    Scanner player = new Scanner(System.in); //The person guessing the word
    boolean first=false,second=false,third=false,fourth=false;
    int misses = 0;
    
    //The Game Part
    //While the player doesn't have a full body hanged or the full word. Keep asking for a new letter
    while(misses!=6 && (first==false || second==false || third==false || fourth==false)){
      printHanging(misses);
      printWord(word,first,second,third,fourth);
      System.out.println("Guess a letter");
      char a = player.next().charAt(0);
      
      int guess=isLetterInWord(word,a);
      if(guess==0){
        first=true;
      }
      else if(guess==1){
        second=true;
      }
      else if(guess==2){
        third=true;
      }
      else if(guess==3){
        fourth=true;
      }
      else{
        misses++;
      }
    }
    //Display the final results
    printHanging(misses);
    printWord(word,first,second,third,fourth);
    
    //If they ended up with a full body hanged
    if(misses==6){
      System.out.println("Sorry. Better luck next time");
    }
    //If they guessed the word
    else{
      System.out.println("Horray! You Won!");
    }
    
    
    player.close();
  }
}
