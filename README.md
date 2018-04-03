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
            Console.WriteLine("YAHTZEE");//Start of Yahtzee Instructions. This will display on the console when the program runs. 
            Console.WriteLine("");
            Console.WriteLine("Yahtzee is a popular dice game.");
            Console.WriteLine("");
            Console.WriteLine("The objective of this game is to roll 5 dice to create high scoring");
            Console.WriteLine("combinations. There are a total of 13 rounds. For each round, the");
            Console.WriteLine("player can roll the dice one time. After rolling, the player");
            Console.WriteLine("chooses what category they would like their combination to be scored");
            Console.WriteLine("under. However, once you pick a category, you cannot choose it again.");
            Console.WriteLine("");
            Console.WriteLine("Try and score the highest possible score. Have fun and good luck!"); //End of Yahtzee Instructions
            while (playGame) //Loop for the start game message
            {
                menuCommand = DisplayMenu();//DisplayMenu() references the menu command that starts and closes the game 

                switch (menuCommand.ToUpper())//Conditional Statement. "ToUpper" allows it the "X" to be case insensitive.
                {
                    case "X"://if the user presses X
                        playGame = false;//then the game closes 
                        break;
                    default: //Otherwise
                        PlayYahtzee();//the game begins and the PlayYahtzee() function starts. 
                        break;
                }

            }
        }
        static string DisplayMenu()
        {
            {
                string menuCommand = "";

                Console.WriteLine("");//menu command to start or exit the game 
                Console.WriteLine("- press 'Enter' to start the game");
                Console.WriteLine("- press 'X' to exit");
                Console.WriteLine("");

                menuCommand = Console.ReadLine();//Readline waits for user to press enter or x. 
                return menuCommand;//Returns menucommand (start/close menu) whenever the game starts. 
            }
        }

        static string CategoryMenu()
        {
            {
                string menuCommand2 = "";//second menu command: This menu shows the different categories that can be selected. Once a category is selected, it calculates the score for that category. 
                                         //We wanted to include a condition so that the user is restricted to one category per game. 
                                         //However, we had difficulty implementing this. Based on the sources we found, we could have used an if/then statement or readkey in order to restrict the key selected.  
                Console.WriteLine("");
                Console.WriteLine("- press (1) to choose Aces");
                Console.WriteLine("- press (2) to choose Twos");
                Console.WriteLine("- press (3) to choose Threes");
                Console.WriteLine("- press (4) to choose Fours");
                Console.WriteLine("- press (5) to choose Fives");
                Console.WriteLine("- press (6) to choose Sixes");
                Console.WriteLine("- press (7) to choose Three of a Kind");
                Console.WriteLine("- press (8) to choose Four of a Kind");
                Console.WriteLine("- press (9) to choose Small Straight");
                Console.WriteLine("- press (10) to choose Large Straight");
                Console.WriteLine("- press (11) to choose Full House");
                Console.WriteLine("- press (12) to choose Chance");
                Console.WriteLine("- press (13) to choose Yahtzee");
                Console.WriteLine("");

                menuCommand2 = Console.ReadLine();//Waits for the user to press a key. 
                return menuCommand2;//Returns menuCommand2 (category menu) once round starts. 
            }
        }

        private static void PlayYahtzee()//This is where the actual game is coded. 
        {

            int grandTotal = 0;//integer keeps track of the total of all rounds. The grand total is updated every round.  
            for (int i = 1; i <= 13; i++)//this establishes the 13 rounds of Yahtzee
            {
                int[] dr = new int[6]; //this establishes the 6 sides of the dice 
                string categoryCommand = "";
                int total = 0;//Creates integer that will track the total of the upper section
                int threetotal = 0;//Creates integer that will track the total of three of a kind 
                int fourtotal = 0;//Creates integer that will track the total of four of a kind
                int yahtzeetotal = 0;//Creates integer that will track the total of yahtzee
                int smalltotal = 0;//Creates integer that will track the total of the small straight
                int largetotal = 0;//Creates integer that will track the total of the large straight
                int fulltotal = 0;//Creates integer that will track the total of the full house
                int chancetotal = 0;//Creates integer that will track the chance 
                Console.WriteLine("Round: " + i);//Title of each round
                Random rndGen = new Random(); //Generates random dice "rolls"

                Console.WriteLine("\nDice Rolls: ");
                for (int j = 0; j < 5; j++)//This establishes the five dice 
                {

                    System.Threading.Thread.Sleep(500);//It pauses the game for half of a milisecond. Establishes a "rolling" effect.
                    int diceRoll = 0; //Creates integer that rolls the dice 
                    diceRoll = rndGen.Next(6);//5 dice are rolled and a random number is generated for each one of them.
                    dr[diceRoll]++; //add 1 to dr array at index of diceRoll
                    Console.Write("{0,10}", diceRoll + 1);//Has to do with the spacing of the die. 
                                                          //Ideally we would like the user to be able to roll the dice up to 3 times and select which die they would like to keep and which die they would like to roll again. 
                                                          //But, we faced difficulty in coding this. If we were to implement this, we would have to keep track of the dice and the dice values and restrict the number of rolls. 
                }

                categoryCommand = CategoryMenu();//once dice is rolled, the category menu shows up. 
                switch (categoryCommand.ToUpper())//Coding of conditional statements established in category menu. 
                {
                    case "1"://if the aces category is selected 
                        dr[0] = 1 * dr[0];//then 1 is multiplied with the number of 1s rolled. All of the other values are shown as 0. 
                        total = dr[0];//The uppersection total is of the sum of all the aces.  
                        dr[1] = 0;
                        dr[2] = 0;
                        dr[3] = 0;
                        dr[4] = 0;
                        dr[5] = 0;
                        threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                        grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                        break;
                    case "2"://if the twos cateogry is selected
                        dr[1] = 2 * dr[1];//then 2 is multiplied with the number of 2s rolled. All of the other values are shown as 0. 
                        total = dr[1];//The uppersection total is of the sum of all the twos. 
                        dr[0] = 0;
                        dr[2] = 0;
                        dr[3] = 0;
                        dr[4] = 0;
                        dr[5] = 0;
                        threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                        grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                        break;

                    case "3": //if the threes category is selected
                        dr[2] = 3 * dr[2];//then 3 is multiplied with the number of 3s rolled. All of the other values are shown as 0. 
                        total = dr[2];//The uppersection total is of the sum of all the threes. 
                        dr[0] = 0;
                        dr[1] = 0;
                        dr[3] = 0;
                        dr[4] = 0;
                        dr[5] = 0;
                        threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                        grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                        break;
                    case "4": //if the fours category is selected
                        dr[3] = 4 * dr[3];//the 4 is multiplied with the number of 4s rolled. All of the other values are shown as 0.
                        total = dr[3];//The uppersection total is of the sum of all the fours. 
                        dr[0] = 0;
                        dr[1] = 0;
                        dr[2] = 0;
                        dr[4] = 0;
                        dr[5] = 0;
                        threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                        grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                        break;
                    case "5": //if the fives category is selected  
                        dr[4] = 5 * dr[4]; //then 4 is multiplied with the number of 4s rolled. All of the other values are shown as 0. 
                        total = dr[4]; //The uppersection total is of the sum of all the fives. 
                        dr[0] = 0;
                        dr[1] = 0;
                        dr[2] = 0;
                        dr[3] = 0;
                        dr[5] = 0;
                        threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                        grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                        break;
                    case "6"://if the sixes category is selected 
                        dr[5] = 6 * dr[5];//then 6 is multiplied with the number of 6s rolled.All of the other values are shown as 0.  
                        total = dr[5]; //The uppersection total is of the sum of all the sixes. 
                        dr[0] = 0;
                        dr[1] = 0;
                        dr[2] = 0;
                        dr[3] = 0;
                        dr[4] = 0;
                        threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                        grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                        break;
                    case "7":
                        if (dr[0] == 3 || dr[1] == 3 || dr[2] == 3 || dr[3] == 3 || dr[4] == 3 || dr[5] == 3)//Conditional statement where if exactly three dice are the same
                        //the total is the sum of all dice and all the other integers are set to 0.
                        {
                            threetotal = 1 * dr[0] + 2 * dr[1] + 3 * dr[2] + 4 * dr[3] + 5 * dr[4] + 6 * dr[5];
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                            fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                            grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                        }
                        else//if the condition is not met, all of the integers are set to 0 and the grandtotal is not updated. 
                        {
                            threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                        }
                        break;
                    case "8":
                        if (dr[0] == 4 || dr[1] == 4 || dr[2] == 4 || dr[3] == 4 || dr[4] == 4 || dr[5] == 4)//Conditional statement where if exactly four dice are the same
                        //the total is the sum of all dice and all the other integers are set to 0.
                        {
                            fourtotal = 1 * dr[0] + 2 * dr[1] + 3 * dr[2] + 4 * dr[3] + 5 * dr[4] + 6 * dr[5];
                            grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                            threetotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;

                        }
                        else //if the condition is not met, all of the integers are set to 0 and the grandtotal is not updated. 
                        {
                            threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                        }
                        break;
                    case "9":
                        if ((dr[0] == 1 && dr[1] == 1 && dr[2] == 1 && dr[3] == 1) || (dr[1] == 1 && dr[2] == 1 && dr[3] == 1 && dr[4] == 1) || (dr[2] == 1 && dr[3] == 1 && dr[4] == 1 && dr[5] == 1))//conditional statement where if there is four sequential die
                                                                                                                                                                                                       //We were not able to code it so that the program recognizes the order of the dice. However, we were able to code it so the program recognizes the current values that would occur in order to have a sequential order. We realize this is not ideal but it is the best that we could do. 
                                                                                                                                                                                                       //All other integers are set to 0. 
                        {
                            smalltotal = 30;//small straight scores as 30. 
                            grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                            threetotal = 0; fourtotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                        }
                        else //if the condition is not met, all of the integers are set to 0 and the grandtotal is not updated. 
                        {
                            threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                        }
                        break;
                    case "10":
                        if ((dr[0] == 1 && dr[1] == 1 && dr[2] == 1 && dr[3] == 1 && dr[4] == 1) || (dr[1] == 1 && dr[2] == 1 && dr[3] == 1 && dr[4] == 1 && dr[5] == 1))
                        //conditional statement where if there is five sequential die
                        //We were not able to code it so that the program recognizes the order of the dice. However, we were able to code it so the program recognizes the current values that would occur in order to have a sequential order. We realize this is not ideal but it is the best that we could do. 
                        //All other integers are set to 0. 
                        {
                            largetotal = 40;//large straight scores are 40.
                            grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                            threetotal = 0; fourtotal = 0; smalltotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                        }
                        else //if the condition is not met, all of the integers are set to 0 and the grandtotal is not updated.
                        {
                            threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                        }
                        break;
                    case "11":
                        if ((dr[0] == 3 || dr[1] == 3 || dr[2] == 3 || dr[3] == 3 || dr[4] == 3 || dr[5] == 3) && (dr[0] == 2 || dr[1] == 2 || dr[2] == 2 || dr[3] == 2 || dr[4] == 2 || dr[5] == 2))
                        //Conditional statement where if there is three of one number and two of another number
                        //All other integers are set to 0. 
                        {
                            fulltotal = 25;//then the score value is 25. 
                            grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + yahtzeetotal + grandTotal;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                            threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; chancetotal = 0; yahtzeetotal = 0;

                        }
                        else //if the condition is not met, all of the integers are set to 0 and the grandtotal is not updated.
                        {
                            threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                        }
                        break;
                    case "12":
                        chancetotal = 1 * dr[0] + 2 * dr[1] + 3 * dr[2] + 4 * dr[3] + 5 * dr[4] + 6 * dr[5];//Dice can be any combination and the score is the sum of the dice values. 
                        //All other integers are set to 0. 
                        grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                        dr[0] = 0;
                        dr[1] = 0;
                        dr[2] = 0;
                        dr[3] = 0;
                        dr[4] = 0;
                        dr[5] = 0;
                        threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; yahtzeetotal = 0;
                        break;

                    case "13":
                        if (dr[0] == 5 || dr[1] == 5 || dr[2] == 5 || dr[3] == 5 || dr[4] == 5 || dr[5] == 5) //Conditional statement where if all 5 dice are the same value
                        //All other integers are set to 0
                        {
                            yahtzeetotal = 50;//The score is 50
                            grandTotal = total + threetotal + fourtotal + smalltotal + largetotal + fulltotal + chancetotal + yahtzeetotal + grandTotal;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                            threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0;
                        }
                        else //if the condition is not met, all of the integers are set to 0 and the grandtotal is not updated.
                        {
                            threetotal = 0; fourtotal = 0; smalltotal = 0; largetotal = 0; fulltotal = 0; chancetotal = 0; yahtzeetotal = 0;
                            dr[0] = 0;
                            dr[1] = 0;
                            dr[2] = 0;
                            dr[3] = 0;
                            dr[4] = 0;
                            dr[5] = 0;
                        }
                        break;

                }
                Console.WriteLine("\n\nUpper Section");//Scorecard 
                Console.WriteLine("____________________________________________________________________________");
                Console.WriteLine("Aces   Twos   Threes   Fours    Fives    Sixes  ");
                Console.WriteLine(dr[0] + "   "
                                  + "   " + dr[1] + "   "
                                  + "   " + dr[2] + "     "
                                  + "   " + dr[3] + "     "
                                  + "   " + dr[4] + "     "
                                  + "   " + dr[5]);
                Console.WriteLine("____________________________________________________________________________");
                Console.WriteLine("");
                Console.WriteLine("");
                Console.WriteLine("Lower Section");//Scorecard 
                Console.WriteLine("____________________________________________________________________________");
                Console.WriteLine("3 of a Kind   4 of a Kind  Small Straight  Large Straight   Full House ");

                Console.WriteLine(threetotal + "             " + fourtotal + "            " + smalltotal + "               " + largetotal + "                " + fulltotal);
                Console.WriteLine("____________________________________________________________________________");
                Console.WriteLine("Yahtzee    Chance    Grand Total");
                Console.WriteLine(yahtzeetotal + "          " + chancetotal + "         " + grandTotal);
                Console.WriteLine("____________________________________________________________________________");
                //Values from integers are shown within the scoresheet. 

                if (i < 13) //Conditional statement where if the rounds are less than 13
                {
                    Console.WriteLine("- press 'Enter' to roll the 5 dice to start the round");//then this message appears
                    Console.ReadLine();//Waits for the user to press enter
                }
            }
            Console.WriteLine("Congratulations! You have finished the game."); //Otherwise, the game is completed at the 13th round and the user is ideally able to see the prices of the Yahtzee game extracted from Amazon. 
            Console.WriteLine("You score is " + grandTotal + "!");
            Console.WriteLine("If you would like to purchase the game, the prices listed on Amazon are ");

        }
        //WEB SCRAPING EXPLAINATION:

        //1. HtmlAgilityPack serves as a wrapper in C# that allows us to query the DOM and extract the Yahtzee price data
        //2. In line 386, "HtmlWeb" will load the HTML of the given URL using HTTP.
        //3. Line 389 includes the anchor tag element and class name from the DOM and it is converted to a list
        //4. Line 392 will will loop through the list and call the "InnerText" prpperty of each item in the list
        //5. When the code below runs, it should extract all the different price options of the Yahtzee game from Amazon. This way, the user can see the different price options in case they want to purchase the game.

        // WEB SCRAPING CODE: 

        //HtmlAgilityPack.HtmlWeb web = new HtmlAgilityPack.HtmlWeb();
        //HtmlAgilityPack.HtmlDocument doc = web.Load("https://www.amazon.com/s/ref=nb_sb_noss_2/136-9872247-2467866?url=search-alias%3Daps&field-keywords=yahtzee");
        //var PriceNum = doc.DocumentNode
        //.SelectNodes("//a[@class='sx-price sx-price-large']").ToList();
        //foreach (var item in PriceNum)
        //{
        //Console.WriteLine("\nIf you would like to purchase the game, the prices listed on Amazon are" + item.InnerText);
        //}

    }
}
