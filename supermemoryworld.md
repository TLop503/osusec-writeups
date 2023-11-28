### 11/27/23
# Super Memory World (pwn)

1. For this challenge we are given the source code for a sidescrolling platformer game, and an ssh for the game itself. Inspecting the code shows us that the gamespace is a finite array without anything checking for collsions at the borders. Navigating through the player through the level and then back over some clouds to the start allows you to jump off the edge, wrapping back around to the other side where the flag is stored.

2. Challenge 2 is much more complicated. There isn't a way to escape the level. Instead, you have to collect a certain amount of "money" to open a door, specifically equal to the hexadecimal values for a few keys scattered in the level. Normally when you pick up a key it is added to an array, but if you pick up a key after filling the array it overflows into the money value. Using this information you can determine the order keys need to be collected, gaining the specific amount of mone neccessary and unlocking the door to the flag.
