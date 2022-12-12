# keepoffthegrass

## Codingame fall challenge 2022

### We need concepts of `game loop` and `before game loop`

### Step 1: Verify 'width' and 'height'

* Notice a game board: rectangle of spaces
* Notice code above the game loop: mentions width and height
* Let's print them, also above the game loop
    * Borrowing from the future: The squares are indexed using Python indexing (from 0)
    * Does the board wrap around???

### Step 2: Run the game and observe

* There is both a *score* at the top and a *gear* number
    * I bet the gear number is build resources!
    * I bet the score is how many squares we control
        * High score at the end of the last turn wins
    * Sometimes squares have a **`2`** on them
        * Maybe 2 bots stacked together?
    * There is a scrollbar to the right of the game board
        * Rules!!! (skip this for now)

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


