# Snake-Ocaml
Classic snake game using OCaml
#+TITLE: Snake

* Introduction
  Snake is a video game where the player maneuvers a line (the snake)
  around a screen. The goal is to grow the snake's length by eating
  apples that are randomly generated on the screen. 

  The snake constantly moves forward. Users can interact with the game
  by changing the direction of the snake. The controls are:
  - [w] -> go up
  - [s] -> go down
  - [a] -> go left
  - [d] -> go right

  The player loses if the snake collides with the walls or itself. The
  player wins if the snake fills the entire screen, so that no apples
  can be generated.


* Code Overview
  We have implemented a simple event-loop that drives the game and
  handles graphic rendering as well as keyboard input in
  [[file:bin/snake.ml][snake.ml]]. Feel free to take a look to get a sense of how the game
  engine works under the hoodl.


** ~Snake.t~
   A [Snake.t] represents a snake on the game board.

** ~Apple.t~
   An [Apple.t] represents an apple on the game board.

** ~Game.t~
   A [Game.t] represents the entire game state, including the current
   [snake] and [apple]. Make sure to look at [[file:lib/game.mli][game.mli]] to understand
   its structure.

   Please note! In this model, we treat the origin of the playing area
   as its lower left hand corner.

* Expect Tests
  This game makes use of expect tests to test functions individually
  and ensure that they are all working properly.

  In practice, when you run the expect tests in a file ~my_file.ml~, if there is
  any difference in output, dune will create a file ~my_file.ml.corrected~. You
  can then diff the two files to see what changed between what the original file
  expected and what was actually produced.

  You shouldn't need to write or change any expect tests while working
  on these exercises, but they may be helpful for debugging purposes
  while writing code. 

* Getting Started
  The functions for you to implement are in
  - [[file:lib/direction.ml][direction.ml]]
  - [[file:lib/apple.ml][apple.ml]]
  - [[file:lib/snake.ml][snake.ml]]
  - [[file:lib/game.ml][game.ml]]

  To compile the tests, run (from the root directory of the snake project):

  #+BEGIN_SRC bash
  $ dune runtest
  #+END_SRC

  For this exercise, tests are split into three directories corresponding to the
  three phases outlined in [[Order of Implementation]]. It may be helpful while
  going through the exercises to run only the subset of tests corresponding to
  the phase you are working on by specifiying a directory when running
  tests. For example:

  #+BEGIN_SRC bash
  $ dune runtest tests/phase1
  #+END_SRC
  
  Note that the runtest target will only show the expect test diff for the
  first file that has a diff. To see the diff for a specific file, you can run 
  
  #+BEGIN_SRC bash
  $ (cd _build/default && /usr/bin/diff -u tests/phase1/snake_tests.ml tests/phase2/snake_tests.ml.corrected)
  #+END_SRC
  
  (See [[Expect Tests]] for an explanation on ~.ml.corrected~ files.) 
   
  To run the game, run (from the root directory of the snake project):

  #+BEGIN_SRC bash
  $ dune exec bin/snake.exe
  #+END_SRC

  Note that during the course of this exercise, you will be able to 
  run the game even when not all tests pass. This might be helpful for
  development and debugging.

* Order of Implementation
  A suggested ordering for working through this game (though feel free
  to do in a different order if you prefer) is:

** Phase 1: Initial Rendering
   - [ ] [[file:lib/apple.ml][apple.ml]]: [create]
   - [ ] [[file:lib/snake.ml][snake.ml]]: [create]
   - [ ] [[file:lib/snake.ml][snake.ml]]: [locations]
   - [ ] [[file:lib/game.ml][game.ml]]: [in_bounds]
   - [ ] [[file:lib/game.ml][game.ml]]: [create]

   At the end of phase 1, you should be able to see the initial board
   get rendered with an apple and a snake. Additionally, all expect tests 
   for phase 1 should pass:

   #+BEGIN_SRC bash
   $ dune runtest tests/phase1
   #+END_SRC

   Recall that you can see expect test diffs for specific files by running:

   #+BEGIN_SRC bash
   $ (cd _build/default && /usr/bin/diff -u tests/phase1/snake_tests.ml tests/phase2/snake_tests.ml.corrected)
   #+END_SRC

** Phase 2: Utilities
   - [ ] [[file:lib/direction.ml][direction.ml]]: [next_position]
   - [ ] [[file:lib/snake.ml][snake.ml]]: [grow_over_next_steps]
   - [ ] [[file:lib/snake.ml][snake.ml]]: [head_location]
   - [ ] [[file:lib/snake.ml][snake.ml]]: [set_direction] 
   - [ ] [[file:lib/game.ml][game.ml]]: [set_direction]

   At the end of phase 2, all expect tests for phase 2 should pass:

   #+BEGIN_SRC bash
   $ dune runtest tests/phase1
   #+END_SRC

** Phase 3: Game Progression
   - [ ] [[file:lib/snake.ml][snake.ml]]: [step]
   - [ ] [[file:lib/game.ml][game.ml]]: [step]

   At the end of phase 3, you should be able to play snake in its
   entirety and also pass all expect tests:

   #+BEGIN_SRC bash
   $ dune runtest
   #+END_SRC

* Extensions
  Once your game is working, there are many fun extensions that you
  can try to implement!

  Some examples, for inspiration:
  - calculate and display a score
  - make the snake change color 
  - make apples "time out" and disappear
  - make special apples that have a different effect on the length of
    the snake
