# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable.

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the fixed app: `python3 -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** The secret number was being converted to a string on every even attempt. This caused even number guesses to fail silently and never be recorded in the history.
3. **Fix the Logic.** The hints were completely backwards. Guessing too high said "Go HIGHER" and guessing too low said "Go LOWER". I fixed check_guess() so the messages match the correct direction.
4. **Refactor & Test.** Moved get_range_for_difficulty(), parse_guess(), check_guess(), and update_score() from app.py into logic_utils.py. Ran pytest and fixed all issues until all 3 tests passed.

## 📝 Document Your Experience

**What is the game?**
A number guessing game where the player chooses a difficulty and guesses a number within a range. The game gives hints after each guess and tracks the score. Easy is range 1-20, Normal is 1-100, and Hard is 1-200.

**Bugs I found:**
1. Hints were backwards — Too High said "Go HIGHER" and Too Low said "Go LOWER"
2. Even number guesses were skipped due to a string vs integer conversion bug
3. New Game button did not reset score, history, or game status
4. Hard difficulty used range 1-50 which was easier than Normal
5. Info text always showed "1 and 100" regardless of difficulty selected
6. All game logic was mixed inside app.py instead of logic_utils.py

**Fixes I applied:**
1. Swapped messages in check_guess() so hints are now correct
2. Removed string conversion code and always passed secret as an integer
3. Updated New Game button to reset all session state
4. Changed Hard difficulty range to 1-200
5. Replaced hardcoded numbers with {low} and {high} variables
6. Moved all logic functions into logic_utils.py

## 📸 Demo



## 🚀 Stretch Features

**Challenge 2: Feature Expansion via Agent Mode**

I used Agent Mode to plan and implement a Guess History sidebar that shows how close each previous guess was to the secret number. This gives the player better visual feedback during the game. The agent helped plan the feature and I reviewed every change it made before accepting.