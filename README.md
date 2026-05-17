# Hangman — C++ Console Game

> **Group Member 2's Game**
> AI Disclosure: Claude (Anthropic) assisted with structure and ASCII art gallows. All game logic is student work.

---

## Overview

A classic Hangman game implemented in C++ as a console application. The player guesses a hidden word letter by letter before the stick figure is fully drawn on the gallows (6 wrong guesses allowed).

---

## Features

- 7-stage ASCII gallows animation
- Word list loaded from an external file (`hangman_words.txt`)
- Built-in fallback word list (15 CS/programming terms) if file is missing
- Case-insensitive input — type upper or lowercase freely
- Duplicate guess detection
- Replay support — keep playing rounds without restarting
- Minimum word length filter (4+ characters)

---

## OOP Concepts Demonstrated

| Concept | Where |
|---|---|
| **Inheritance** | `Hangman` derives from `Game` base class |
| **Composition** | `Hangman` owns a `WordLoader` member object |
| **File I/O** | `WordLoader` reads words from `hangman_words.txt` |
| **Encapsulation** | Game logic split across private helper methods |

---

## File Structure

```
project/
├── Game.h              # Base class (provided by instructor)
├── Hangman.h           # Hangman game — WordLoader + Hangman classes
└── hangman_words.txt   # (Optional) One word per line, 4+ letters
```

---

## How to Compile & Run

```bash
# Compile
g++ -o hangman main.cpp

# Run
./hangman
```

> Make sure `Game.h` and your `main.cpp` (which instantiates `Hangman`) are in the same directory.

---

## Word File Format

`hangman_words.txt` should contain one word per line:

```
programming
computer
algorithm
variable
```

Words shorter than 4 letters are automatically skipped. Words are converted to uppercase internally. If the file is missing or empty, the game falls back to a built-in list of 15 programming/CS terms:

```
POLYMORPHISM, INHERITANCE, ENCAPSULATION, ABSTRACTION,
COMPILER, ALGORITHM, RECURSION, POINTER, TEMPLATE,
ITERATOR, OVERLOADING, CONSTRUCTOR, DESTRUCTOR,
VARIABLE, FUNCTION
```

---

## Gameplay

```
  +---+
  |   |
  O   |
 /|\  |
 /    |
      |
=========

Word: _ _ _ _ _ _ _ _ _ _
Guessed: A E I
Wrong left: 2
Guess a letter:
```

- Enter one letter at a time and press Enter
- Non-letter input is rejected
- Already-guessed letters are flagged
- The word is revealed on win or loss

---

## Game Rules

| Condition | Result |
|---|---|
| Guess all letters correctly | **Win** — word is displayed |
| 6 wrong guesses | **Lose** — full gallows drawn, word revealed |
| Repeated guess | Warning shown, turn not consumed |
| Non-letter input | Warning shown, turn not consumed |

---

## Dependencies

- C++11 or later
- Standard library only (`<iostream>`, `<fstream>`, `<vector>`, `<string>`, `<algorithm>`, `<cctype>`, `<cstdlib>`)
- `Game.h` base class from the course project

---

## Known Limitations

- Single-player only
- No score tracking across sessions
- `rand()` used for word selection — not cryptographically random (fine for a game)
