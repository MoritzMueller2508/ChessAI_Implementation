# *Chess AI Implementation*

## Section 1: About

This repository logs the development of an AI for the popular and challenging game **chess**.
This group project is being developed by two students enrolled in the Baden-Württemberg Cooperative State University Mannheim as part of bachelor programme *applied computer science*.

In the following, the original task given by professor [Karl Stroetmann](https://github.com/karlstroetmann/) is presented.  
Although the original description is in German, it has been translated to English for the purpose of this ReadMe.

---

## Section 2: Task - Development of a Chess AI

Chess is the most popular board game in the western world. The goal of this project is to develop a chess AI.
In this project, one must implement the evaluation function described at

[https://www.chessprogramming.org/Simplified_Evaluation_Function](https://www.chessprogramming.org/Simplified_Evaluation_Function)

alongside alpha-beta pruning and transposition tables.
Both of these topics are discussed in prof.
Stroetmann's script titled ["Introduction to Artificial Intelligence"](https://github.com/karlstroetmann/Artificial-Intelligence/raw/master/Lecture-Notes/artificial-intelligence.pdf).
In order to achieve acceptable performance, it is important to implement a so-called Quiescence Search:

[https://www.chessprogramming.org/Quiescence_Search](https://www.chessprogramming.org/Quiescence_Search)

The AI should be developed using the library

[https://pypi.org/project/python-chess/](https://pypi.org/project/python-chess/).

This library should also be used as the GUI. The program should be developed as Jupyter Notebooks.

---

## Section 3 - Quickstart

To run the Notebooks and dive into the world of computer chess, follow the instructions below:  

**1. Set up your python environment**  

Firstly, set up a conda virtual environment with 

    conda create --name 'your_desired_name' python=3.10.4 pip

After that, simply use the **requirements.txt** file to install all necessary modules with pip.

    pip install -r requirements.txt

Please bear in mind that this requirements.txt can only be installed with the package installer for Python, [pip](https://pypi.org/project/pip/).  
Anaconda does not provide the necessary modules, so `conda install --file requirements.txt` **does not work!**

After this environment is set up, simply run

    conda activate your_desired_name
    
to activate the environment. Then, run

    jupyter notebook
    
to open Jupyter Notebook and access the notebooks of the project. We strongly recommend using Jupyter Notebook, as links to the bibliography do not work in most other environments, including Visual Studio Code.
  
**2. Download the Gaviota endgame tablebases**  
Due to the size of the Gaviota endgame tablebases, these files cannot be uploaded to GitHub.
However, it is very simple to include the endgame tablebases.  

First, download the [library files](https://drive.google.com/file/d/1ZDuEx8Tl6u6Rcy7wasMSwe9ysEGwSF8U/view?usp=sharing). After downloading, unzip the package into the "Resources" folder (ChessAI_Implementation/Resources). After extracting, there should now be a folder called "Gaviota" in Resources, which contains .gtb.cp4 files for the endgame tablebases.  

Please note that the endgame tablebases takes up 6.54GB, so it may take some time to download the files depending on your Internet connection.

**3. Start a game**  
After the Python environment is ready, simply head over to **Play.ipynb** to play a game of chess against the current most sophisticated algorithms.

You can also create your own game by creating a `Game` object:

    game = Game.Game(*params)

A game can be initialized with different algorithms as well as other parameters.
The available search algorithms are listed below. For more information on these algorithms, see their respective notebooks, or the notebook summaries at the bottom of this ReadMe. 

1. `RandomAlgorithm`: an algorithm that makes a random legal move.
1. `NegamaxSearch`: pure negamax search: a simple, but slow algorithm.
1. `NegamaxSearchMemo`: negamax search with memoization (caching). 
1. `AlphaBetaPruning`: negamax search with alpha-beta pruning: an optimized version that cuts off useless branches in the search tree.
1. `AlphaBetaPruningMemo`: negamax search with alpha-beta pruning and memoization (caching).
1. `AlphaBetaPruningPD`: negamax search with alpha-beta pruning, memoization and progressive deepening, which iteratively increases the search depth to sort moves by their estimated score, allowing more branches to be pruned.  
1. `AlphaBetaPruningQuiescence`: negamax search with alpha-beta pruning, memoization, progressive deepening and quiescence search, which prevents the search from ending directly after a capturing move. 
This lets the algorithm detect protected pieces, therefore making it more intelligent. However, it also makes the search time slower and less consistent. An overview of the advantages and disadvantages of this version can be found in AlphaBetaAlgorithm.ipynb.

The different paramaters a game can be initialized with are listed below.

``algorithm_white (type[ChessAlgorithm], default: None):``  
The class of the chess algorithm that the white pieces should use to make a new move, or `None` if the white pieces are player-controlled.  

``algorithm_black (type[ChessAlgorithm], default: None):``  
The class of the chess algorithm that the black pieces should use to make a new move, or `None` if the black pieces are player-controlled. 

``search_depth_white (int, default: 4):``  
The search depth for the white AI's search algorithm. It is recommended to set this to a lower value for negamax search without alpha-beta pruning, or if quiescence search is enabled, in order to make search times realistic. 

``search_depth_black (int, default: 4):``  
The search depth for the black AI's search algorithm. It is recommended to set this to a lower value for negamax search without alpha-beta pruning, or if quiescence search is enabled, in order to make search times realistic. 

``opening_book (str, default: 'Resources/baron30.bin'):``  
The path to the desired opening book the AIs will use, or `None` if no opening book is desired.

``endgame_tablebase_dir (str, default: 'Resources/Gaviota'):``  
The path to the directory of the desired endgame tablebases the AIs will use, or `None` if no endgame tablebases are desired.

``use_heuristic (bool, default: True):``  
Whether or not to use a heuristic to evaluate moves. This is only `False` in the context of chess problems, where only checkmates need to be considered.

``fen (str, default: None):``  
The FEN code representing the state that the chess board should start in, or `None` if it should start with the standard starting layout.  

It is recommended not to set the `opening_book` and `endgame_tablebase_dir` arguments to `None`, in order to reduce the time needed by the AI to make a move during the opening and to allow the AI to make more intelligent moves during the endgame.
Not providing any parameters will result in an error, because at least one player in a game has to be an AI.

---

## Section 4: Order of Python Notebooks

In order to use the program, only the `Play.ipynb` notebook needs to be run.
However, if one wants to take a closer look at the implemented algorithms and functionality, the order for reading should be:

1. **Introduction.ipynb**
1. **Globals.ipynb**
1. **ChessAlgorithm.ipynb**
1. **Game.ipynb**
1. **RandomAlgorithm.ipynb**
1. **Evaluation.ipynb**
1. **TestUtil.ipynb**
1. **EvaluationTests.ipynb**
1. **Util.ipynb**
1. **NegamaxAlgorithm.ipynb**
1. **NegamaxTests.ipynb**
1. **AlphaBetaAlgorithm.ipynb**
1. **AlphaBetaTests.ipynb**
1. **MiscTests.ipynb**  
1. **Play.ipynb**
1. **Conclusion.ipynb**
1. **Bibliography.ipynb**

---

## Section 5: Summary of Each Notebook

In the following, each Python notebook is briefly described. This should give a general understanding about the structure and content of each notebook.

---

### *Section 5.1: Introduction.ipynb*

**Introduction.ipynb** describes the overall goal of the project and the requirements that came with it. This notebook also contains definitions which establish a base required for understanding the different algorithms and the evaluation function. To be precise, the notebook defines a **Two-player-zero-sum-game with perfect information** as well as **Heuristic** functions.

---

### *Section 5.2: Globals.ipynb*

**Globals.ipynb** contains general constants which are used by the evaluation function, the search algorithms and some tests. Therefore, the contained variables are globally accessible and should not be modified at runtime.  
A detailed explanation of each constant can be found in the markdown cells in this notebook.

---

### *Section 5.3: ChessAlgorithm.ipynb*

**ChessAlgorithm.ipynb** contains the `ChessAlgorithm` class, which is a base class for all chess AI search algorithms. This class contains the base structure for such an algorithm, including information that all algorithms share, such as endgame tablebases.
The different algorithms extend this base class, implementing a search in different ways.

---

### *Section 5.4: Game.ipynb*

**Game.ipynb** contains the `Game` class, a central class to manage games of chess. It contains various methods to play a game of chess and manage the board. A `Game` object contains an AI algorithm that a human can play against using a visual interface, or two AI algorithms that automatically play against each other. After the `Game` object has been created with the desired options and parameters, a game of chess can be played with the `Game.play` method.  

---

### *Section 5.5: RandomAlgorithm.ipynb*

**RandomAlgorithm.ipynb** contains a simple algorithm that executes a random legal move. This means that this algorithm can only execute moves which comply with the rules of chess, but does not evaluate these moves.

---

### *Section 5.6: Evaluation.ipynb*

**Evaluation.ipynb** contains methods for evaluating a move on a chess board.
These methods are used by all search algorithms (except the random algorithm), which is why they are defined in an external notebook and then made accessable to each algorithm.

---

### *Section 5.7: TestUtil.ipynb*

**TestUtil.ipynb** contains various methods for testing, which range from support functions to full game tests.

---

### *Section 5.8: EvaluationTests.ipynb*

**EvaluationTests.ipynb** contains tests for verifying the correctness of the evaluation function.

---

### *Section 5.9: Util.ipynb*

**Util.ipynb** contains various helper functions for search algorithms and move evaluation. 
These functions are used by multiple notebooks, therefore they are defined in their own separate notebook and can be imported as necessary.

---

### *Section 5.10: NegamaxAlgorithm.ipynb*

**NegamaxAlgorithm.ipynb** implements the [negamax search algorithm](https://www.chessprogramming.org/Negamax) as well as a version with memoization.
The negamax algorithm determines a score for each possible move in a two-player zero-sum game with perfect information using an evaluation function and finds the best possible move to take. 
It looks at all possible moves in the future (up to a given search depth, i.e. a fixed number of half-moves) and finds the move that leads to the highest score after this number of half-moves, assuming perfect play by the opponent.
The memoization version saves the already evaluated moves in a cache, so that further evaluations can be done more efficiently, reducing the overall search time in most instances.

---

### *Section 5.11: NegamaxTests.ipynb*

**NegamaxTests.ipynb** contains tests for verifying the correctness of the negamax search algorithm with and without memoization. It also measures the performance of these algorithms.

---

### *Section 5.12: AlphaBetaAlgorithm.ipynb*

**AlphaBetaAlgorithm.ipynb** implements the negamax search algorithm with [alpha-beta pruning](https://doi.org/10.1016/0004-3702(75)90019-3).  
Alpha-beta pruning is an optimization that can be applied to negamax search. It "cuts off" (prunes) unnecessary branches in the search, optimizing the search.
This notebook also contains variations that implement memoization, [progressive deepening](https://www.chessprogramming.org/Iterative_Deepening) and [quiescence search](https://www.chessprogramming.org/Quiescence_Search).

---

### *Section 5.13: AlphaBetaTests.ipynb*

**AlphaBetaTests.ipynb** contains and performs tests for verifying the correctness of the negamax search algorithm with alpha-beta pruning, including the variations with memoization, progressive deepening and quiescence search.
Furthermore, it compares negamax search with and without alpha-beta pruning in order to verify that alpha-beta pruning speeds up the search. It also measures the performance of alpha-beta pruning and its variations.

---

### *Section 5.14: MiscTests.ipynb*

**MiscTests.ipynb** contains and performs tests for verifying the correctness of miscellaneous features. Specifically, it tests the following:
- The opening book integration.
- The endgame tablebase integration.
- The uniqueness of the board state representation.
- Saving and loading games.

---

### *Section 5.15: Play.ipynb*

**Play.ipynb** is a simple notebook that lets the user play a game of chess against the current most sophisticated algorithms.
It presents the option to play either with or without quiescence search. Both of the presented algorithms utilize negamax search with alpha-beta pruning, memoization and progressive deepening. Quiescence search makes the algorithm more intelligent, but also makes the search time less consistent, therefore this choice is given to the player depending on what they value more.

---

### *Section 5.16: Conclusion.ipynb*

**Conclusion.ipynb** summarizes the performance of the search algorithms, draws general conclusions about the project and discusses potential further optimizations.

---

### *Section 5.17: Bibliography.ipynb*

**Bibliography.ipynb** contains all literature referenced in the various notebooks. 