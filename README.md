﻿# Console.Menu
CSharp console menu allows you to quickly and easily organize a complex menu.

## Features

### Navigation
![Imgur](https://i.imgur.com/OzcHtiO.png)

### Dynamic
![Imgur](https://i.imgur.com/BqrrLkv.png)

### Input
![Imgur](https://i.imgur.com/L0FNzQY.png)

### Confirm
![Imgur](https://i.imgur.com/v3wgUsI.png)

### Program

```c#
using Nim.Console;
using System;
using System.Text;

namespace MenuTest
{
    class Program
    {
        static Menu Menu;

        static void Main(string[] args)
        {
            Console.OutputEncoding = Encoding.Default;

            Menu = new Menu
            (
                "Main",
                new[]
                {
                    new Menu.Item("Static", new[]
                    {
                        new Menu.Item("Sub-0", Print),
                        new Menu.Item("Sub-1", Print),
                        new Menu.Item("Sub-2", Print),
                        new Menu.Item("Sub-3", Print)
                    }),
                    new Menu.Item("Dynamic", Generate),
                    new Menu.InputItem("Input Test", "Please input you name", InputTest),
                    new Menu.Item("Confirm", Print){ ActionIfConfirmed = true },
                    new Menu.Item("Exit", Exit),
                }
            );

            Menu.Main.MaxColumns = 1;
            
            Menu.WriteLine("Use ←↑↓→ for navigation.");
            Menu.WriteLine("Press Esc for return to main menu.");
            Menu.WriteLine("Press Backspace for return to parent menu.");
            Menu.WriteLine("Press Del for clear log.");

            Menu.Begin();
        }

        static void Print()
        {
            Menu.WriteLine("Selected: " + Menu.Selected.Name);
        }
        
        static void Generate()
        {
            if (Menu.Selected.Items.Count > 0)
            {
                return;
            }


            for (var i = 0; i < 50; ++i)
            {
                var sub = new Menu.Item("Dynamic - " + i, Print);
                

                Menu.Selected.Add(sub);
            }
        }

        static void InputTest(string str)
        {
            var inp = Menu.Selected as Menu.InputItem;

            Menu.WriteLine("You wrote: " + inp.Value);
        }

        static void Exit()
        {
            Menu.Close();
        }
    }
}

```
![Imgur](https://i.imgur.com/OPDjcpd.png)
