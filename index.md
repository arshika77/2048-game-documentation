# Documentation
## _Welcome to the official documentation for the 2048 game engine DevelopedBy@Arshika_

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

The game engine is an interpreter based program that initializes a random 2048 matrix at every new run of the script and then takes input from the user in a line-by-line manner. The game engine runs in the following manner:

- Initialize a random state 2048 matrix
- Take input from the user
- Parse user input
- Perform the appropriate function as indicated by the parser
- Raise any syntax or semantic error that the user commits
- Provide suggestions to the user if any errors occur
- If function executes, change the state of the 2048 matrix
- Continue steps 2 to 6 in till the user stops the terminal using the Ctrl+C signal
- EOF can be used to exit from the shell

> The rules of the general 2048 game
> can be found [here](https://en.wikipedia.org/wiki/2048_(video_game)#Gameplay) . This game engine
> is designed for the 2048 game and the
> 2048 "family" of games. Thus, it contains
> several commands to introduce variations
> in the original 2048 gameplay

###### Note: The developer can choose the board dimensions at will in the interactiveshell.py file. The default dimension is a 4x4 board.

## List of commands

The commands in the language specification for this game engine are case-sensitive. The "." indicated End of Line (EOL). The following is the list of commands with a brief description:

#### ADD 
The ADD command adds two rows/coloumns of tiles element-by-element             in a particular direction. The tiles can be added irrespective of whether they hold same or different values
    _Syntax_:  ADD DIRECTION .
    Values of DIRECTION allowed: LEFT, RIGHT, UP, DOWN

#### SUBTRACT / MULTIPLY / DIVIDE
These commands perform their respective operations on two rows/coloumns of tiles element-by-element in a particular direction. However, unlike the ADD operation, the tiles can be operated on only if they hold same values. If the tiles hold different values, a normal 2048 move is played on them. The general rules for 2048 can be found [here](https://en.wikipedia.org/wiki/2048_(video_game)#Gameplay)
    _Syntax_:  SUBTRACT/MULTIPLY/DIVIDE DIRECTION .
    Values of DIRECTION allowed: LEFT, RIGHT, UP, DOWN
    
Note: The SUBTRACT command leads to the creation of empty tiles.
#### ASSIGN
The assignment operator sets a tile value to the value given by the user. The function checks if the co-ordinates for assignment are valid, and does an assignment if they are valid, and throws an error if they are not
_Syntax_:  ASSIGN <VALUE> TO <X,Y> .

#### VAR
The naming operator assigns names to the tiles. A tile can have multiple names stacked on it, depending on the 2048 oves being played. If a tile value goes to 0 (say due to the SUBTRACT operation), then all the tile names are dropped. Keywords are not allowed to be used as tile names.
_Syntax_:  VAR <VARNAME> IS <X,Y> .

#### VALUE IN 
The query operator is used to extract the value held in a given tile. Both the tile coordinates and the tile name can be used to extract the tile value. In case of multiple tile names, any tile name can be used to the extract the value.
_Syntax_:  VALUE IN <X,Y> .
_Syntax_:  VALUE IN <TILENAME> .

The query operator can also be used within an assignment operator
_Syntax_: ASSIGN VALUE IN <X,Y> TO <X',Y'> .

## List of Errors

The game engine can raise the following errors:

- "The keyword 'X' cannot be used as a variable name" : This error is thrown if the user is using the VAR command with a keyword X. Keywords cannot be used as tile names, retry with a different tile name
- "The command must end with a \".\" " : This error is thrown if the user has written a command without the EOL character (.) .  All commands must contain the EOL character.
- "some command" must be in uppercase" - The game engine language is case sensitive. All commands must be written in upper-case. 
- "SYNTAX ERROR: Please check your syntax around X" - This error is thrown if an unrecognised character or string X is used.
- "Ran into an unexpected X. Please check your syntax" - The game engine cannot place the source of syntax error
- "Coordinates out of range. Coordinates must be in the range (0,dim)": Valid coordinates lie in the range [0,dim). Default dimension is 4. 
- "Cannot assign tile name to empty tile": Tiles with empty or 0 values cannot be assigned names.
- "Cannot name tile. Tile name <TILENAME> already exists ": Duplicate tile names are not allowed.

##### From the README:

## Installing the requirements

Install the dependencies for the game engine.

```sh
pip install -r requirements.txt
```

## Running the game engine shell

```sh
python interactiveshell.py
```

#### Game assumptions:
- **0 - based - indexing**: The coordinate system of the 2048 game starts from (0,0) and not from (1,1). This is because 0-based indexing is what is followed in the world of computer science(that is the actual game grid and tile name grid are 0-indexed in python) , making it easier for developers to add more functionality without having to deal with the headache of 1-indexing. A 1-based-indexing would have made it difficult for developers to keep track of the actual indices of the game matrix, and I did not want to impose such restrictions. It is easier to switch from 0-based indexing to 1-based indexing, and hence I felt 0-based indexing would be a more useful design choice.
- **SUBTRACT operation implementation**: The subtract operation will run in the following manner:

                    4 2 2 4
                    0 0 0 0
                    0 0 0 0
                    0 0 0 0 
                    
            ---> SUBTRACT LEFT
                
                    4 4 0 0
                    0 0 0 0 
                    0 0 0 0
                    0 0 0 0
            [NOTE: In actual implementation, a random tile will also be added]

- **Representation of an empty tile**: The numerical character '0' represents an empty tile. This is because after the SUBTRACT operation, a tile would be set to 0, and will not produce any relevant results on using any of the action moves. Thus, the tile is as good as empty. To not create two different representations of the empty tile, a design choice was made to represent empty tile using '0'. Note, empty tiles cannot be assigned tile names. If a tile is set to 0 after the SUBTRACT operation, all its tile names are freed.
- **STDERR OUTPUT**: The stderr output is printed after every command, and is printed on stderr (which prints on the terminal), instead of redirecting to a file. This is so that the stderr output can be redirected from the command line itself if required.
- **Two tiles cannot have the same tile name**: Allowing repeated tile names would lead to ambiguity in command <VALUE IN TILENAME> and in any further functions that the developer writes using the tracked tiles. Thus, a design choice was made to disallow same tile name for multiple tiles.

#### Reasons for choosing Python as the language
Since the language is not very complex, and has only a countable number of statements and commands, a slower language (relative to C/C++) was not an issue. However, python offers much better support for handling matrices and grids, due to its ability of vectorization, and thus produces code which is much more optimized for a 2048-game-engine. Python-Lex-Yacc (PLY) is a a straightforward lex/yacc implementation entirely in Python.It uses LR-parsing which is reasonably efficient and well suited for larger grammars as well. It provides most of the standard lex/yacc features including support for empty productions, precedence rules, error recovery, and support for ambiguous grammars, and is a very close implementation of the two in Python. I have used RPLY in this project, which is an updated version of PLY.

## Built in partial fulfillments of the course

```sh
CS F363: Compiler Construction
```




