## Iteration 1

Big Picture — What is this code trying to do?

The code is retrieving step-by-step instructions for making mashed potatoes and adding each step to a webpage in the correct order.
Why does it need this structure?
Because getInstruction() is asynchronous — meaning it doesn’t return the result immediately. It likely simulates a network request (like fetching from an API).
So the program must wait for step 0 before asking for step 1, then wait again before step 2, etc.
👉 Think of it like cooking with someone reading instructions over the phone — you can’t hear the next step until they finish the previous one.

🔹 Walkthrough (mentally execute it)

1️⃣ First call
getInstruction("mashedPotatoes", 0, (step0) => {

👉 “Give me step 0, and when you have it, run this function.”
When the step arrives:
document.querySelector("#mashedPotatoes").innerHTML += `<li>${step0}</li>`;

✔️ It finds the HTML element with id mashedPotatoes
✔️ Adds a <li> containing the instruction

2️⃣ Immediately inside that callback…

It requests step 1:
getInstruction("mashedPotatoes", 1, (step1) => {

Same pattern repeats.
Each step is nested inside the previous callback so execution stays in order.

🔹 Why not just do this?
You might wonder:
getInstruction(0)
getInstruction(1)
getInstruction(2)

Because async calls can finish in random order.
Without nesting you could get:
Step 3
Step 1
Step 0
Step 2

Not great for cooking

🔹 The Final Step
After step 4:
document.querySelector("#mashedPotatoesImg").style.display = "block";

This reveals the image — probably hidden with display: none.

🔹 The Real Lesson Here (important)
This code works…
…but it has a major structural problem.
Look at the shape:
callback
 └ callback
    └ callback
       └ callback

This is called:
👉 Callback Hell
👉 Pyramid of Doom

Why developers avoid it:
✅ Hard to read
✅ Hard to debug
✅ Hard to maintain
✅ Error handling becomes messy
✅ Doesn’t scale
Imagine 15 steps instead of 5 😬

🔹 How modern JavaScript fixes this
Today we prefer:
✅ Promises
or even better…
✅ async / await

Which turns that pyramid into clean, top-to-bottom logic.
Example (just conceptually):
const step0 = await getInstruction(...)
const step1 = await getInstruction(...)

Reads like synchronous code. Much easier for your brain.

## Iteration 2