# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
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

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.


# Reflection: Game Glitch Investigator

## 1. What was broken when you started?

When I first ran the game it looked normal but immediately felt wrong. The hints were completely backwards — when I guessed a number that was too high the game told me to go higher, and when I guessed too low it told me to go lower. This made it impossible to win by following the hints. I also noticed that even number guesses like 2, 4, 6, 8 were being skipped entirely — I typed the numbers 1 through 15 but the history only showed 7 entries. The New Game button also did not reset the score or history, so old game data carried over into new games.

---

## 2. How did you use AI as a teammate?

I used GitHub Copilot inside VS Code throughout this project. I gave it context by using #file:app.py and #file:logic_utils.py in every prompt so it could see both files at once. One correct suggestion was when I asked Copilot to fix the backwards hints — it correctly identified that the messages in check_guess() were swapped and fixed them so Too High returns "Go LOWER!" and Too Low returns "Go HIGHER!" I verified this by playing the game and confirming the hints matched my guesses. One incorrect suggestion was when Copilot kept the logic in update_score() that gave the player +5 points for a wrong guess on even attempts. This made no sense because wrong guesses should always lose points. I rejected this and told Copilot to always return -5 for wrong guesses, then verified the score went down consistently after each wrong guess.

---

## 3. Debugging and testing your fixes

I decided a bug was really fixed by testing it in two ways — first by playing the game manually in the browser, and second by running automated pytest tests. For the even number bug I typed 1, 2, 3, 4, 5, 6, 7 one by one and checked that all 7 appeared in the history with no skipping. For automated testing I wrote 3 pytest tests in tests/test_game_logic.py that checked winning, too high, and too low outcomes. Running pytest tests/test_game_logic.py -v showed all 3 tests passing which confirmed the core logic was working correctly. Copilot helped me understand what the tests should check and why each assertion mattered.

---

## 4. What did you learn about Streamlit and state?

The secret number kept changing because every time the player clicked Submit, Streamlit completely reloaded the entire app from the top. This meant the secret number was being randomly regenerated on every click instead of staying the same. Streamlit reruns are like refreshing a webpage — every button click causes the whole script to run again from scratch. Session state is like a small memory box that survives these reruns, so anything stored in st.session_state stays the same between clicks. The fix was storing the secret number inside st.session_state when the game first starts, so it only gets created once and stays the same for the whole game.

---

## 5. Looking ahead: your developer habits

One habit I want to reuse in future projects is writing clear and specific AI prompts that include the exact broken code and what I want instead. Vague prompts gave me vague answers, but when I showed Copilot the exact lines and explained the expected behavior it gave much better fixes. Next time I work with AI on a coding task I would write automated tests before trying to fix anything, so I can immediately run the tests after each fix and know if it worked instead of manually testing everything in the browser. This project changed the way I think about AI generated code because I used to assume AI code would just work — now I know it can have hidden logic bugs that look fine on the surface but break in specific situations that you only catch by actually running and testing the code.