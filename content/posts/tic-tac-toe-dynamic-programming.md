---
draft: false
date: 2016-06-24
title: Tic-tac-toe dynamic programming
tags: reinforcement learning, dynamic programming
---

This is the first of many articles regarding reinforcement learning, which is something I want to master. I will try to do it using ["Reinforcement learning", by Richard Sutton and Andrew Barto][2] as a reference. The objective of a reinforcement learning system is building a program that learns rather than the much more usual, the human learns and teaches the computer the result of its learning.

As with everything, first steps are humble: the tic-tac-toe game. The book does not provide an implementation. I found however [this nice implementation][1] using dynamic programming:

```python
def build_best_responses(self, board=None, player=None):
    """Recursively compute best responses for all subgames of current board.

    Call with no arguments to build the entire best_responses dict.

    This adds a key to best_responses for each possible board configuration
    that could follow from board.

    player = 1 for X, -1 for O. This is the current player, i.e. the one
    who goes next given the current board.
    """

    # Initialize
    if board is None:
        board = (0,) * self.SIZE
        player = 1

    if board in self.best_responses:
        return

    win = self.check_win(board, player)
    # If win/loss/draw has been determined, the game is over.
    if win is not None:
        self.best_responses[board] = (None, win) # None => no move needed
        return

    # If we don't know the best response yet, compute it.
    best_value = -2
    for i, val in enumerate(board):
        if val == 0:
            # create new tuple with player's move in ith slot
            board2 = board[:i] + (player,) + board[i+1:]

            # If board2 is already in best_responses, this does nothing.
            # Otherwise, it ensures board2 is added to best_responses.
            self.build_best_responses(board2, -1 * player)
            # The player's value given board2 is the reverse of the next
            # player's value
            value = -1 * self.best_responses[board2][1]
            if value > best_value:
                best_value, best_move = value, i
    self.best_responses[board] = (best_move, best_value)
```

Is this reinforcement learning? What this code does is for any board composition it computes the value of the board, and it starts with the empty board. So effectively it is enumerating all the possible states, something that can be done for simple games like tic-tac-toe.

Being able to evaluate all posible states makes it possible to evaluate the game in a deterministic way, which makes finding the best policy easy. The difficulty of reinforcement learning, I guess, is determining this "board value", it will not always be simple.

[1]: https://www.xanvong.com/posts/blog/tic-tac-toe-dp-and-memo
[2]: https://webdocs.cs.ualberta.ca/~sutton/book/the-book.html