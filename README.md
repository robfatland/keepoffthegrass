# keepoffthegrass

## Codingame fall challenge 2022


* [ideas, experiments](https://github.com/robfatland/keepoffthegrass/blob/main/IdeasAndCode.md)


Before we get started: It is a good idea to stretch our minds a bit.
We will do two stretches.


### First stretch


Let's discuss space. 


- One-D: If my program gives your program a list: You can search for 'Gladys'.
    - This space has one dimension...
        - An entry in a list
        - A location on a line
- What if Gladys is a bot living somewhere on a grid?
- What if Gladys is a fish in an aquarium?
- What if we add time?


### Second stretch


- `game loop` is a concept related to turns
    - the challenge game will resolve moves simultaneously
- `before game loop` is related to setting up the pieces
    - like for monopoly or chess


### Step 1: Let's verify 'width' and 'height'


* Notice a game board: rectangle of spaces
* Notice code above the game loop: mentions width and height
* Let's print them, also above the game loop
    * Borrowing from the future: The squares are indexed using Python indexing (from 0)
    * Does the board wrap around???


### Step 2: Run the game and observe


* There is both a *score* at the top and a *gear* number
    * I bet the gear number is build resources!
    * I bet the score is how many squares we control
        * High score at the end of the last turn wins?
    * Sometimes squares have a **`2`** on them
        * Maybe 2 bots stacked together?
    * There is a scrollbar to the right of the game board
        * Rules!!! (skip this for now)
* If we start the game over with **Play my code**: New game board!
    * We seem to be blue always; but our start quadrant changes
    * Let's call the four quadrants **LL**, **UL**, **LR**, **UR**


> Pro Tip: The video is actually playback; it is not 'real time'
    

### Step 3: Run the code and see what our opponent is up to


* Opponent issues several commands separated by semicolons `;`
    * Scroll back and forth in `stdout` window to see the game progress
    * Scroll left and right for a command to see its details
    * `WAIT` is allowed: Just sit there
    * `BUILD <x> <y>` builds a factory (*Recycler*) on an empty square
    * `MOVE <n> <x> <y> <a> <b>` moves a bot located at <x> <y>
    * `SPAWN <n> <x> <y>` creates a new bot at <x> <y>
        * Does <n> mean 'the number of bots on this square'?
        * Why are <a> and <b> always 1 and 2?

   
### Step 4: Read the rules!

   
* Aha! The game is about recycling junk to reveal a nice grassy field
* In the `MOVE` command, `<a> <b>` is the to-square
    * The game figures out the most efficient path for us
        * We do not need to do 'maze path solving'
    * We need information on which corner of the board we live on
        * This is a kind of global orientation
        * In the arena we might start in the upper left or the lower right
* Each game loop, at the start: We receive information about the entire game board
    * We can use this information to make decisions
   
   
> ***REALIZATION: During the board scan we can make our own copy of all the information!!!***

   
### Step 5: Print out the game board size

```
print("width: " + str(width) + "     height: " + str(height), 
    file=sys.stderr, flush=True)
```
   
   
### Step 6: Let's roll!!!


We know we have four units; let's try to head for the corner!


This goes inside the game loop above the nested for-i / for-j loop:


```
botx = []
boty = []
```


This goes inside the nested for-i / for-j loop: It records bot locations in two lists.


```
if owner == 1:
   for k in range(units):
       botx.append(j)
       boty.append(i)
```

This replaces the print('WAIT') statement at the bottom of the game loop. Be sure to indent it so it is part of the game loop.


```
msg = ''
nbots = len(botx)
for i in range(nbots):
   start_location = str(botx[i]) + ' ' + str(boty[i]) + ' '
   end_location = str(i) + ' 0;'
   msg = msg + 'MOVE 1 ' + start_location + end_location
print(msg)
```
   
Add these to the basic program and see if the bots do as they are instructed.


