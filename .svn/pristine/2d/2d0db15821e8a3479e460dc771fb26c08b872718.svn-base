//******************************************************************
//Berton Quon CMPE 1300 Lab 2
//******************************************************************

using System;
using GDIDrawer;
using System.Drawing;

namespace Lab_2
{
    class Program
    { 
        static void Main(string[] args)
        {
            int borderTop;              //creates top border
            int borderRight;            //creates right border
            int borderBottom;           //creates bottom border
            int xBall;                  //x position of ball
            int yBall;                  //y position of ball
            int yStart;                 //starting direction of yBall
            int xVel;                   //x velocity of ball (constant velocity)
            int yVel;                   //y velocity of ball (constant velocity)
            int startClick;             //do-while loop to start game
            bool startGame;             //boolean to get mouse click to reset game
            int score;                  //score counter
            bool yPaddle;               //collect y position of mouse for paddle position
            bool replay;                //boolean to replay game
            bool postGame;              //boolean to create options after game ends
            int postGameClick;          //clicking during postgame to decide what happens after game ends

            //************************************************************************
            //create game window
            CDrawer canvas = new CDrawer();
            canvas.Scale = 5;
            //create top border
            for (borderTop = 0; borderTop < 160; borderTop++)
            {
                canvas.SetBBScaledPixel(borderTop, 0, Color.Blue);
            }
            //create right border
            for (borderRight = 0; borderRight < 120; borderRight++)
            {
                canvas.SetBBScaledPixel(159, borderRight, Color.Blue);
            }
            //create bottom border
            for (borderBottom = 0; borderBottom < 160; borderBottom++)
            {
                canvas.SetBBScaledPixel(borderBottom, 119, Color.Blue);
            }
            //*************************************************************************
            do
            {
                //reset values
                Console.Clear();
                replay = false;
                xVel = 1;
                yVel = 1;
                score = 0;
                startClick = 0;
                postGameClick = 0;

                //add start (able to click anywhere in game console to start game)
                canvas.AddRectangle(65, 55, 30, 10, Color.Green, 5, Color.Yellow);
                canvas.AddText("Click to start", 12, 65, 55, 30, 10, Color.White);
                Point pCoord;
                do
                {
                    startGame = canvas.GetLastMouseLeftClickScaled(out pCoord);
                    if (startGame)
                        ++startClick;
                }
                while (startClick != 1);
                //*************************************************************************
                //game starts
                //generate ball at random location
                Random rand = new Random();
                xBall = rand.Next(2, 159); //randomized x spawn location of ball
                yBall = rand.Next(1, 119); //randomized y spawn location of ball
                yStart = rand.Next(1, 3); //determine initial y direction of ball

                while (xBall >= 0 && xBall < 160)
                {
                    canvas.Clear(); //clear old values

                    yPaddle = canvas.GetLastMousePositionScaled(out pCoord);
                    if (pCoord.Y < 11) //create top limit of paddle in game console
                        pCoord.Y = 11;
                    if (pCoord.Y > 109) //create bottom limit of paddle in game console
                        pCoord.Y = 109;

                    canvas.AddRectangle(1, (pCoord.Y - 10), 1, 20, Color.Brown); //create paddle 

                    canvas.AddRectangle(xBall, yBall, 2, 2, Color.Red); //create ball
                    System.Threading.Thread.Sleep(20); //add delay 
                    xBall = xBall + xVel;

                    switch (yStart)
                    {
                        case 1: //ball moves downwards at start
                            yBall = yBall + yVel;
                            break;
                        case 2: //ball moves upwards at start
                            yBall = yBall - yVel;
                            break;
                        default:
                            break;
                    }
                    if (xBall == 157)
                        xVel = -xVel; //changes ball to leftward direction
                    if (yBall == 117 || yBall == 1)
                        yVel = -yVel; //changes ball to opposite vertical direction 
                    if (xBall == 1 && yBall < (pCoord.Y + 10) && yBall > (pCoord.Y - 10)) //ball hits paddle
                    {
                        xVel = -xVel; //change direction of ball
                        score++; //add to score counter
                    }
                }

                //end game when xBall position = 0, and display score 
                if (xBall < 0)
                {
                    canvas.Clear();
                    canvas.AddText($"Final Score: {score} ", 36, 35, 40, 80, 30, Color.Gray);
                }

                //display buttons to play again or quit
                Point click;
                canvas.AddRectangle(80, 100, 30, 10, Color.Black, 1, Color.GreenYellow); //replay button
                canvas.AddText("Replay", 18, 80, 90, 30, 30, Color.White);
                canvas.AddRectangle(120, 100, 30, 10, Color.Black, 1, Color.DarkRed); //quit button
                canvas.AddText("Quit", 18, 120, 90, 30, 30, Color.White);
                
                do
                {
                    postGame = canvas.GetLastMouseLeftClickScaled(out click);
                    if (click.X >= 80 && click.X <= 110 && click.Y >= 100 && click.Y <= 110) //replay
                    {
                        replay = true;
                        postGameClick++;
                    }
                    if (click.X >= 120 && click.X <= 150 && click.Y >= 100 && click.Y <= 110) //quit
                    {
                        canvas.Close();
                        postGameClick++;
                    }
                }
                while (postGameClick != 1);
                canvas.Clear();
            }
            while (replay == true);            
        }
    }
}
