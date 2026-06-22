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

- [x] Describe the game's purpose.
- [x] Detail which bugs you found.
- [x] Explain what fixes you applied.

The game asks the player to guess a secret number within a limited number of attempts. Each guess gets a hint (Too High / Too Low) to guide the next guess. Difficulty controls the number range and attempt limit.

**Bugs found:**
- Hints were backwards (Too High said "Go Higher", Too Low said "Go Lower")
- On even-numbered attempts the secret was cast to a string, breaking comparison
- New Game button did not reset status, score, or history — game stayed locked after win/loss
- New Game ignored difficulty and always picked from 1–100
- Attempts display was off by one (initialized to 1 instead of 0)
- Hard difficulty had a smaller range (1–50) than Normal (1–100)

**Fixes applied:**
- Swapped the Go HIGHER/LOWER messages in check_guess
- Removed the even-attempt string conversion
- New Game now resets status, score, history, and uses the correct difficulty range
- Attempts initialized to 0; display updated via st.empty() placeholder after submit
- Corrected difficulty ranges: Easy 1–20, Normal 1–50, Hard 1–100
- Refactored all logic into logic_utils.py; app.py imports from it

## 📸 Demo Walkthrough

Describe your fixed game in numbered steps so a reader can follow along without watching a video:

1. Run the app with `python -m streamlit run app.py` and select a difficulty from the sidebar.
2. Open the "Developer Debug Info" expander to see the secret number and attempt count.
3. Type a guess in the text box and click "Submit Guess" — a hint tells you to go Higher or Lower.
4. Keep guessing using the hints until you match the secret number exactly to win.
5. Click "New Game" to reset the score, history, and secret — the game is immediately playable again.

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

```
# Paste your pytest output here, e.g.:
# pytest tests/
tests\test_game_logic.py ...                                                                                                                                       [100%]

=========================================================================== 3 passed in 0.11s ===========================================================================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
