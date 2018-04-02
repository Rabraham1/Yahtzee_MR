# Yahtzee_MR
using System;

namespace Yahtzee_Project
{
    class Program
    {
        static void Main(string[] args)
        {
            
            bool playGame = true;
            string menuCommand = "";
            Console.WriteLine("YAHTZEE");
            Console.WriteLine("");
            Console.WriteLine("Yahtzee is a popular dice game.");
            Console.WriteLine("");
            Console.WriteLine("The objective of this game is to roll 5 dice to create high scoring");
            Console.WriteLine("combinations. There are a total of 13 rounds. For each round, the");
            Console.WriteLine("player can roll the dice up to three times. After rolling, the player");
            Console.WriteLine("chooses what category they would like their combination to be scored");
            Console.WriteLine("under. However, once you pick a category, you cannot choose it again."); 
            Console.WriteLine("");
            Console.WriteLine("Try and score the highest possible score. Have fun and good luck!"); //Explaining the rules of the game to the player           
            while (playGame) //Loop for start round message 
            {
                menuCommand = DisplayMenu();

                switch (menuCommand.ToUpper())
                {
                    case "X":
                        playGame = false;
                        break;
                    default:
                        PlayYahtzee();
                        break;
                }

            }
        }
        static string DisplayMenu()
        {
            {
                string menuCommand = "";

                Console.WriteLine("");
                Console.WriteLine("- press 'Enter' to roll the 5 dice to start the round");
                Console.WriteLine("- press 'X' to exit");
                Console.WriteLine("");

               menuCommand = Console.ReadLine();
               return menuCommand;
            }
        }

        static string CategoryMenu()
        {
            {
                string menuCommand2 = "";

                Console.WriteLine("");
                Console.WriteLine("- press (1) to choose Aces");
                Console.WriteLine("- press (2) to choose Twos");
                Console.WriteLine("- press 'X' to exit");
                Console.WriteLine("");

                menuCommand2 = Console.ReadLine();
                return menuCommand2;
            }
        }

        private static void PlayYahtzee()
        {
            
            int[] dr = new int[6];
            Random rndGen = new Random();
            Console.Clear();
            

            for (int i = 0; i<5; i++)
            {
               
                System.Threading.Thread.Sleep(500);//It pauses the game for half of a milisecond 
                int diceRoll = 0;
                diceRoll = rndGen.Next(6);
                dr[diceRoll]++; //add 1 to dr array at index of diceRoll 
                Console.Write("{0,5}", diceRoll + 1);
                
            }
            CategoryMenu();
            Console.WriteLine("\n\nUpper Section");
            Console.WriteLine("_______________________________________________________________");
            Console.WriteLine("Aces   Twos   Threes   Fours    Fives    Sixes     Total");
            Console.WriteLine("");
            Console.WriteLine("_______________________________________________________________");
            Console.WriteLine("");
            Console.WriteLine("");
            Console.WriteLine("Lower Section");
            Console.WriteLine("_______________________________________________________________");
            Console.WriteLine("\n3 of a Kind   4 of a Kind   Small Straight   Large Straight  ");
            Console.WriteLine("");
            Console.WriteLine("_______________________________________________________________");
            Console.WriteLine("");
            Console.WriteLine("");
            Console.WriteLine("_______________________________________________________________");
            Console.WriteLine("Yahtzee    Chance     Total   Grand Total");
            Console.WriteLine("");
            Console.WriteLine("_______________________________________________________________");
        }
    }
}
