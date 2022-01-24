# *Chess_AI Implementation*
---

## Section 1: About

This Repository contains the development of an AI for the popular and challening game **chess**. This project is a group-project of two people - students enrolled in the "Duale Hochschule Baden Württemberg" as part of their studies for the bachelor of _applied computer science_.

In the following, you can see the original task given to us by our professor [__Karl Stroetmann__](https://github.com/karlstroetmann/). Although this is a german version, a summary will be given in english.

---
___[German]___
## Section 2: Task - Entwicklung einer KI für das Schach-Spiel 

Das Schach-Spiel ist in der westlichen Welt das am weitesten verbreitete Brett-Spiel. Ziel der Studienarbeit ist die Entwicklung einer KI für das Schach-Spiel. Bei dieser Studienarbeit geht es darum, die auf der Seite

[https://www.chessprogramming.org/Simplified_Evaluation_Function](https://www.chessprogramming.org/Simplified_Evaluation_Function)

dargestellte Evaluierungsfunktion zusammen mit Alpha-Beta-Suche und Transpositions-Tabellen zu implementieren. Diese beiden Themen werden in meinem Skript über "Introduction to Artificial Intelligence" diskutiert. Um eine akzeptable Performanz der KI zu erreichen, ist es wichtig, dass bei der Suche auch eine sogenannte Ruhesuche (Englisch: Quiescence Search)

[https://www.chessprogramming.org/Quiescence_Search](https://www.chessprogramming.org/Quiescence_Search)

durchgeführt wird.

Die KI soll mit Hilfe der Bibliothek

[https://pypi.org/project/python-chess/](https://pypi.org/project/python-chess/)

entwickelt werden. Diese Bibliothek soll auch als GUI verwendet werden. Das Programm soll als Jupyter Notebook entwickelt werden.

[English]
## Section 2: Task - Development of a chess-AI

Chess is one of the most popular board-game in the western world. The goal of this project is the development of an AI, able to play and compete in chess. In this project, you have to implement the following [evaluation-function](https://www.chessprogramming.org/Simplified_Evaluation_Function) together with the alpha-beta-search and transposition-tables.  
Both of these topics are discussed in professor stroetmanns lecture about [artificial intelligence](https://github.com/karlstroetmann/Artificial-Intelligence/raw/master/Lecture-Notes/artificial-intelligence.pdf).  

In order to archive a aceptable performance, a so called [quiescence-search](https://www.chessprogramming.org/Quiescence_Search) has to be implemented as well.


The AI shall be developed with the [python-chess](https://pypi.org/project/python-chess/) library. 
This library should also be used as gui.  
The program has to be developed as a jupyter notebook.

---

## Helpfull Links

- [Simplified Evaluation Function](https://www.chessprogramming.org/Simplified_Evaluation_Function)
- [An Introduction to Artificial Intelligence](https://github.com/karlstroetmann/Artificial-Intelligence/raw/master/Lecture-Notes/artificial-intelligence.pdf)
- [Quiescence Search](https://www.chessprogramming.org/Quiescence_Search)

---

## Section 3: Order of Python-Notebooks

Each Notebook will be briefly described in the following section. However, in Order to use the program, only the "Test.ipynb" notebook is necessary. 
In addition to that, if a deeper understanding is desired, the respected order for reading should be:

1. __Constants__
2. __RandomAlgorithm__
3. __Util__
4. __MinimaxAlgorithm__
5. __AlphaBetaAlgorithm__
6. __Game__
7. __Test__

---

## Section 4: Summary of each Notebook

In the following, each Python-Notebook will be briefly descriped. This should give a general understanding about the structure and content of each ipynb-notebook.

---

### _Section 4.1: Constants/Globals_
The __Constants.ipynb__ contains general, global constants which are used by the differenc algorithms. Therefore, the contained variables are globally accessable and should not be changed.   
These variables are:  

1. __piece values__  
Each chess-piece has a certain value associated with it. This is important to calculate the score of the moves the AI is able to take.
2. __piece_square_tables__
Each chess-piece has different move-patterns. Therefore, each chess-piece is more valuable at a certain position on the board.  
This means, that there are ideal and bad positions for different chess-pieces on the board.  
Here, piece_square_tables contains a table for every chess-piece-category.
3. __chess_problems__
Chess_problems is a dictionary containing different fen-codes for chess-problems. These problems were made public in different chess-magazines and papers.  
The source for these problems is the [yacpdb](https://www.yacpdb.org/#static/home) - __Yet Another Chess Problem Database__ - which is a web-collection of many different chess-problems.
---
### _Section 4.2: RandomAlgorithm_
The __RandomAlgorithm.ipynb__ contains methods for a simple algorithm, which will execute a random legal move. This means, that this algorithm can only execute moves, which comply with the rules of chess.

---

### _Section 4.3: Util_
The __Util.ipynb__ contains different functions which support the different algorithms.  

This means, that the different algorithms use these functions to evaluate the score of the move the AI might take, as well as the general state of the game. In general, __Util.ipynb__ contains basic functions which all algorithms rely on.

---

### _Section 4.4: MinimaxAlgorithm_
The __MinimaxAlgorithm.ipynb__ contains the [minimax_search-algorithm](https://www.chessprogramming.org/Minimax) as well as a version with memoization.  
The minimax-algorithm determines a score for each possible move in a [zero-sum game](https://en.wikipedia.org/wiki/Zero-sum_game) in regards to an evaluation function and calculates the best possible move to take.  

While the regular implementation of minimax is an algorithm to evaluate possible moves and decide which move to take based on the score of the move, the version with memoization contains a form of caching.  
Therefore, the memoization-version saves the already evaluated moves in a cache-like storage, so that further evaluations can be done more efficiently. 

---

### _Section 4.5: AlphaBetaAlgorithm_
The _AlphaBetaAlgorithm.ipynb_ contains the [alpha-beta-pruning-algorithm](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning#:~:text=Alpha%E2%80%93beta%20pruning%20is%20a,%2C%20Go%2C%20etc.).  

Alpha-beta-pruning aims to decrease the number of moves that are evaluated by the minimax-algorithm. Therefore, the alpha-beta-search-algorithm is more efficiant in terms of time than the minimax-algorithm.  
The concept of alpha-beta-pruning is to stop evaluating a move when at least one possible move has been found, which contains a higher score then the previous one, due to this score already been outperformed by the newly evaluated move.  

Furthermore, this notebook contains a version of alpha-beta-pruning using the concept of iterative deepening. This means that instead of searching every possible move out of every possible move, it iterates over a range between 1 and a maximum depth limit. On each iteration, the algorithm calculates the best possible move using alpha-beta-pruning with regards to the current maximum depth.

---

### _Section 4.6: Game_
The _Game.ipynb_ contains the Game-class, a central class to manage chess-instances.  

The __Game-class__ contains various methods to play a game of chess and manage the board. Through this class, a Game-object can be initialized, consisting of none, one or multiple algorithms that can be played against. After the Game-object has been created with the desired options and parameters, a game of chess can be played with Game.play().   

In addition to that, the Game-class contains a debug-section which enables the developers to do further debugging of possible bugs and features.

---

### _Section 4.6: Test_
The _Test.ipynb_ is the desired place to test the algorithms and play a decent game of chess against your friends, AIs or just to watch different AIs play against each other.  

Furthermore, this is the place the developers test the efficiency and correctness of the different algorithms.

---


## Section 5 - Quickstart
To dive into the world of chess and play a decent game of the worlds most popular board-game follow the instructions below:

__1. set up your python environment__  

To set up your python envirenment, simply use the requirements.txt file to install all necessary python-modules.

    pip install -r requirements.txt


Please bear in mind, that this requirements.txt can only be installed with the Package installer for Python - [pip](https://pypi.org/project/pip/).   
Anaconda does not provide the necessary modules, so

    conda install --file requirements.txt

__does not work!__
  
    

__2. start a game__  
After the python-environment is ready, simply head over to __Test.ipynb__ to start a game of chess.

initialize a Game-object through

    game = Game.Game(...)
and fill in your desired parameters, which are descriped in the notebook.

After that, use game.play() to start the game.  
Have fun!