# Debug Log

**Explain how you used the the techniques covered (Trace Forward, Trace Backward, Divide & Conquer) to uncover the bugs in each exercise. Be specific!**

In your explanations, you may want to answer:

- What is the expected vs. actual output?
- If there is a stack trace, what useful information does it contain?
- Which technique did you use, on which line numbers?
- What assumptions did you have about each line of code, and which ones were proven to be wrong?

_Example: I noticed that the program should show pizza orders once a new order is made, and that it wasn't showing any. So, I used the trace forward technique starting on line 13. I discovered the bug on line 27 was caused by a typo of 'pzza' instead of 'pizza'._

_Then I noticed another bug ..._

## Exercise 1

To debug this exercise, open a terminal `cmd + j` and navigate to the `exercise-1` folder, then run:

```zsh
$ pip3 install virtualenv
$ virtualenv venv-ex1
created virtual environment
$ source venv-ex1/bin/activate
(venv-ex1) ➜  exercise-1 git:(main) ✗ pip3 install -r requirements.txt
```

Then to run the server:

```zsh
python3 app.py
```

## Exercise 2

To debug this exercise, open a terminal `cmd + j` and navigate to the `exercise-2` folder, then run:

```zsh
$ pip3 install virtualenv
$ virtualenv venv-ex2
created virtual environment
$ source venv-ex2/bin/activate
(venv-ex2) ➜  exercise-2 git:(main) ✗ pip3 install -r requirements.txt
```

Then run the server and open the app.py file:

```zsh
python3 app.py
```

1. add a ```.env``` file to the ```exercise-2``` directory.
2. Lines 39 & 40 requesting the city and units input from our form needs to be changed from ```users_ciy``` & ```requested_units``` to ```city``` & ```units``` respectively.
3. Change the ```place``` param to ```q``` on Line 45.
4. Change ```['main]['temperature']``` to ```['main]['temp']``` on line 54.

## Exercise 3

[[Your answer goes here!]]
