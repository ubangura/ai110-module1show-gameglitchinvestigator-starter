# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

I understand this game is a number guessing game where the player tries to guess a secret number.

**Bugs Found:**

- Flipped Hint Logic: In my first test run, I checked the debug info for the secret. I guessed 7, and the hint said to go lower, but the secret was 92. In another game, I guessed 32, and the hint said to go higher, but the secret was 31. This made me think that the comparison operators in the hint logic might be flipped.
- "Attempts" Off by +1: I noticed that the "Attempts" field in the debug info was off by +1; it allowed for 8 attempts but stopped at 7.
- Score Reset Issue: I also observed that after two wrong guesses, the score reset to 0 instead of decreasing by -10 (or -5 per wrong guess).
- Hard Mode Range Issue: I found that hard mode had a smaller range compared to normal mode, which seemed inconsistent.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

Using GitHub Copilot, Copilot's suggestion was to change the hint text to "Go LOWER!" when the guess was too high and "Go HIGHER!" when the guess was too low, which was correct. I verified the result by running the game and checking that the hints now correctly indicated whether to go higher or lower based on my guesses. Also, verified with pytest cases.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I take three steps:

1. Code Scan: I look over the code to check for logical correctness and errors
2. Pytest: Create a Pytest case
3. Run the Code: Play the game to test if functions properly

For example, after fixing the hint logic, I ran the pytest cases for the `check_guess` function, which showed that the hints were now correct for various guesses. I also played the game manually to confirm that the hints aligned with my guesses and the secret number.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

"Reruns" reruns the entire script to keep the UI up-to-date with state changes. Every button click can update the UI and rerun teh script. But what if want to store some data and not lose it after every click. The session states keeps certain pieces of information we want to remain across reruns. We do store the secret number in session state, but on every even attempt changing the type to a 'str'. So, the user input will be one type and the secret another, leading to a mismatch. Removing the check for even attempts and casting the secret fixed the issue.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

The habit I want to reuse is the three-step debugging process: code scan, pytest, and manual testing. It is easy to want to move quickly and just accept that AI generated code is always correct. This approach helps ensure that I catch both logical errors and user experience issues.

Next time, I would probably be more communicative with the AI, providing more context and asking for explanations of suggestions to better understand the reasoning behind them. I often don't explain my thought process to the AI, which can lead to missing out on valuable insights or suggestions.

What changed in my mind is that AI generated code can be more of a communication process rather than just a tool for generating code. I need to be more active in guiding the AI and evaluating its suggestions, rather than passively accepting them and fixing manually after the fact.
