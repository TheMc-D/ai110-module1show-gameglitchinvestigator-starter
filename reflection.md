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


- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
