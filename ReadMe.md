# *Chess_AI Implementation*
---

## Section 1: About

This repository logs the development of an AI for the popular and challenging game **chess**. This group project is being developed by two students enrolled in the Baden-Württemberg Cooperative State University Mannheim as part of bachelor programme _applied computer science_.

In the following, the original task given to us by professor [__Karl Stroetmann__](https://github.com/karlstroetmann/) is presented. Although the original description is in German, it has been translated to English for the purpose of this ReadMe.

---

## Section 1: Task - Development of a chess AI

Chess is the most popular board game in the western world. The goal of this project is to develop a chess AI. In this project, one must implement the evaluation function described at

[https://www.chessprogramming.org/Simplified_Evaluation_Function](https://www.chessprogramming.org/Simplified_Evaluation_Function)

alongside alpha-beta pruning and transposition tables. Both of these topics are discussed in Prof. Stroetmann's script titled ["Introduction to Artificial Intelligence"](https://github.com/karlstroetmann/Artificial-Intelligence/raw/master/Lecture-Notes/artificial-intelligence.pdf). In order to achieve acceptable performance, it is important to implement a so-called Quiescence Search:

[https://www.chessprogramming.org/Quiescence_Search](https://www.chessprogramming.org/Quiescence_Search)

The AI should be developed using the library

[https://pypi.org/project/python-chess/](https://pypi.org/project/python-chess/).

This library should also be used as the GUI. The program should be developed as Jupyter Notebooks.

---

## Section 2: Order of Python Notebooks

In order to use the program, only the "Test.ipynb" notebook needs to be run. However, if one wants to take a closer look at the implemented algorithms and functionality, the order for reading should be:

1. __Globals.ipynb__
2. __RandomAlgorithm.ipynb__
3. __Util.ipynb__
4. __MinimaxAlgorithm.ipynb__
5. __AlphaBetaAlgorithm.ipynb__
6. __Game.ipynb__
7. __Test.ipynb__

---

## Section 3: Summary of each Notebook

In the following, each Python Notebook will be briefly described. This should give a general understanding about the structure and content of each Notebook.

---

### _Section 4.1: Globals.ipynb_
__Globals.ipynb__ contains general constants which are used by the different algorithms. Therefore, the contained variables are globally accessible and should not be changed.   
A detailed explanation of each constant can be found in the markdown cells in this Notebook. 

---

### _Section 4.2: RandomAlgorithm.ipynb_
__RandomAlgorithm.ipynb__ contains methods for a simple algorithm that executes a random legal move. This means that this algorithm can only execute moves which comply with the rules of chess.

---

### _Section 4.3: Util.ipynb_
__Util.ipynb__ contains different functions which support the different algorithms, primarily minimax and alpha-beta. This ranges from evaluation functions to functions that aid in a search.

---

### _Section 4.4: MinimaxAlgorithm.ipynb_
__MinimaxAlgorithm.ipynb__ implements the [minimax search algorithm](https://www.chessprogramming.org/Minimax) as well as a version with memoization.
The minimax algorithm determines a score for each possible move in a [zero-sum game](https://en.wikipedia.org/wiki/Zero-sum_game) using an evaluation function and finds the best possible move to take. It essentially looks at all possible moves in the future (up to a given number of half-moves) and finds the move that leads to the highest score after this number of half-moves, assuming perfect play by the opponent. 
The memoization version saves the already evaluated moves in a cache, so that further evaluations can be done more efficiently, reducing the overall search time in most instances. 

---

### _Section 4.5: AlphaBetaAlgorithm.ipynb_
__AlphaBetaAlgorithm.ipynb__ implements the [alpha-beta pruning algorithm](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning#:~:text=Alpha%E2%80%93beta%20pruning%20is%20a,%2C%20Go%2C%20etc.).  

Alpha-beta pruning aims to decrease the number of moves that are evaluated by the minimax-algorithm. Therefore, the alpha-beta-search-algorithm is more efficiant in terms of time than the minimax-algorithm.  
Alpha-beta pruning follows the same general idea as minimax. In addition, it cuts a search short if a move's evaluated score is worse than a previous score in the search hierarchy, since following this move is a worse idea than following the previously evaluated move with a higher score.

---

### _Section 4.6: Game.ipynb_
_Game.ipynb_ contains the Game class, a central class to manage games of chess. It contains various methods to play a game of chess and manage the board. A Game object contains an AI algorithm that a human can play against using a visual interface, or two AI algorithms that automatically play against each other. After the Game object has been created with the desired options and parameters, a game of chess can be played with the __Game.play__ method.   

In addition to that, the Game class contains a debug section which enables debugging for the purpose of testing functionality and identifying bugs.

---

### _Section 4.6: Test.ipynb_
_Test.ipynb_ is the Notebook that tests the algorithms. It evaluates algorithms using two types of tests:
1. Performance and effectiveness tests by putting two algorithms up against each other. The winner is registered as well as the amount of time the algorithms took to make their moves.
2. Chess problems that the most effective algorithm must solve. These tests can be seen as unit tests.

Further tests should be added when new algorithms or functionality is implemented.

---


## Section 5 - Quickstart
To run the Notebooks and dive into the world of computer chess, follow the instructions below:

__1. Set up your python environment__  

To set up your Python environment, simply use the __requirements.txt__ file to install all necessary modules.

    pip install -r requirements.txt

Please bear in mind that this requirements.txt can only be installed with the package installer for Python, [pip](https://pypi.org/project/pip/).   
Anaconda does not provide the necessary modules, so

    conda install --file requirements.txt

__does not work!__
  
    

__2. Start a game__  
After the Python environment is ready, simply head over to __Test.ipynb__ to start a game of chess. Either run the Notebook to execute all pre-made tests, or create your own game by creating a Game object:

    game = Game.Game(...)

and fill in your desired parameters, which are described in the Notebook itself. After that, use game.play() to start the game.  


Have fun!