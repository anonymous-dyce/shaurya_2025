---
layout: page
title: Simulation HW
toc: True
permalink: /binary_history/simulationhw
categories: ['CSP Classwork']
---

### Popcorn Hack 1:

```python
import random

def roll_dice():
    return random.randint(1,6)

print("Dice roll:", roll_dice())
```

### Popcorn Hack 2:

```python
import random

def biased_color():
    for i in range(10):
        x = random.randint(1,10)
        if x <= 5:
            print("Red")
        elif x >= 8:
            print("Blue")
        else:
            print("Green")

biased_color()
```

### Homework Hack:

```python
import random

def coin_flip_game():
    player1_heads = 0
    player2_heads = 0
    rounds = 0

    while player1_heads < 3 and player2_heads < 3:
        rounds += 1
        p1_flip = random.choice(["heads", "tails"])
        p2_flip = random.choice(["heads", "tails"])

        if p1_flip == "heads":
            player1_heads += 1
        if p2_flip == "heads":
            player2_heads += 1

        print(f"Round {rounds}: Player 1 - {p1_flip}, Player 2 - {p2_flip}")
        print(f"Heads count: Player 1 - {player1_heads}, Player 2 - {player2_heads}\n")

    if player1_heads == 3:
        print(f"Player 1 wins in {rounds} rounds!")
    else:
        print(f"Player 2 wins in {rounds} rounds!")

coin_flip_game()
```
