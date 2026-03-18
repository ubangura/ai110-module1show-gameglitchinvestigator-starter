# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

This is a simple higher-lower number guessing game. There were a few main bugs:

- Flipped Hint Logic: In my first test run, I checked the debug info for the secret. I guessed 7, and the hint said to go lower, but the secret was 92. In another game, I guessed 32, and the hint said to go higher, but the secret was 31. This made me think that the comparison operators in the hint logic might be flipped.
- "Attempts" Off by +1: I noticed that the "Attempts" field in the debug info was off by +1; it allowed for 8 attempts but stopped at 7.
- Score Reset Issue: I also observed that after two wrong guesses, the score reset to 0 instead of decreasing by -10 (or -5 per wrong guess).
- Hard Mode Range Issue: I found that hard mode had a smaller range compared to normal mode, which seemed inconsistent.

Fixes:

- Fixing the hints was as simple as changing the hint text from "GO HIGHER!" when the user guess was too high to "GO LOWER!" and vice versa.
- Fixing the off by one issue, I changed the initial value for attempts in the session state to 0.

## 📸 Demo

[Winning screen](https://drive.google.com/file/d/1zjSSPuWGCO99KU4AaGS2n4TDtzcb36zz/view?usp=drivesdk)

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, insert a screenshot of your Enhanced Game UI here]
