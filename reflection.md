# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

  A new game cannot be started so you have to refresh/restart the page
  The hint give the opposite of what you are supposed to input
  On every even-numbered attempt the secret number is secretly converted to a string, so the game compares a number to text — this causes the directional hints to be wrong on those turns and can prevent the game from detecting a correct answer properly
  when you start a new game it still shows the you already won message

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
|   50  |    go higher      |   go lower      |       none             |
|   70  |    go higher      |   go lower      |       none             |
|   90  |    go lower       |   go higher     |       none             |
| correct number (attempt 2) | win | wrong hint or no win detected | none — string vs int comparison fails silently |
| Click New Game after win | Fresh game starts | "You already won" blocks play | none — status not reset |
| Select Easy, click New Game | Secret from 1–20 | Secret from 1–100 | none — hardcoded range |
| Fresh load, before any guess | Show 8 attempts left | Shows 7 (off by one) | none — initial attempts=1 |
| Switch to Hard difficulty | Range 1–100 | Range 1–50 (smaller than Normal) | none |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
claude code

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).

Claude correctly identified that the even-attempt string conversion bug was causing hints to break on every second guess. It explained that when `st.session_state.attempts % 2 == 0`, the secret was cast to a string, making a numeric comparison impossible. I verified this by testing: after removing those lines, guesses on even attempts returned correct hints and wins were properly detected.

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

Claude suggested changing the Hard difficulty range to 1–200 to make it genuinely harder than Normal's 1–100. That was the wrong direction — the intended design was Easy: 1–20, Normal: 1–50, Hard: 1–100. I caught it because I knew what the ranges should be, and corrected the suggestion before it was applied.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I decided a bug was fixed by manually playing the game after each change and checking that the behavior matched what was expected — for example, submitting a number lower than the secret and confirming "Go HIGHER" appeared. For the refactor, I ran `python -m pytest tests/` and all 3 tests passed, confirming that `check_guess` returned the correct outcome strings. The tests showed that returning a tuple instead of a plain string would have caused failures, which is exactly why the function signature had to change during the refactor. Claude explained why `python -m pytest` works when `pytest` alone fails — it adds the project root to the Python path so `logic_utils` can be imported.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

Every time you click a button or type something in Streamlit, the entire Python script reruns from top to bottom — like refreshing a webpage but for your code. That means any regular variable you created gets wiped and reset. `st.session_state` is like a notebook that survives those reruns — anything you store in it stays put between clicks. I also learned that because the script runs top to bottom, the order of your code matters: a display that renders before a button handler runs will show stale data unless you use a placeholder like `st.empty()` and update it after the logic runs.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to keep is asking AI to show me the change before applying it. Several times in this project I caught issues — like the wrong difficulty range — because I reviewed the suggestion first instead of just accepting it. Next time I work with AI on a coding task I would test each fix immediately in the running app rather than batching multiple changes before testing, so it's easier to trace which fix caused a new problem. This project showed me that AI-generated code can look completely reasonable and still have multiple subtle bugs — I can't trust it just because it runs without errors.

