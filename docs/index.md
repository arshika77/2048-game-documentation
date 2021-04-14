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

> The rules of the general 2048 game
> can be found [here](https://en.wikipedia.org/wiki/2048_(video_game)#Gameplay) . This game engine
> is designed for the 2048 game and the
> 2048 "family" of games. Thus, it contains
> several commands to introduce variations
> in the original 2048 gameplay

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

## Installing the requirements

Install the dependencies for the game engine.

```sh
python requirements.py
```

## Running the game engine shell

```sh
python test.py
```

## Built in partial fulfillments of the course

CS F401: Compiler Construction
