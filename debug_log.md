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

1. TypeError: 'topping' is an invalid keyword argument for PizzaTopping

2. It only returns ```None``` and a traceback error stating:
        ```werkzeug.routing.BuildError: Could not build url for endpoint '/'. Did you mean 'fulfill_order' instead?```
    - Due to using url_for() we must provide the function name rather than the path in @app.route(). \
    After we update this we are able to navigate back to the main screen after ordering. \
    This solves the traceback but it'd didnt create a pizza as indicated by the size being none.

3. From this we can see that the variables _order__name, pizza__size__str, & toppings__list_ are not being set/grabbed properly.
    - To solve this lets confirm that what we are grabbing is the same as what we are passing back. We need the name of each input to match the value we are looking for in our request statements. \
    From This:

    ```python3
      order_name = request.form.get('name')
      pizza_size_str = request.form.get('size')
      crust_type_str = request.form.get('crust_type')
      toppings_list = request.form.get('toppings')
    ```

    To This:

    ```python3
      order_name = request.form.get('order_name')
      pizza_size_str = request.form.get('pizza_size')
      crust_type_str = request.form.get('crust_type')
      toppings_list = request.form.get('toppings')
    ```

4. One thing I did notice though is that the input for the toppings selection displays that you can select multiple optioins however that isn't accounted for in the html code. This is a simple fix, just add ```multiple``` to the end of the input.

    ```HTML
      <input type="checkbox" name="toppings" value="{{ topping.name }}" multiple>
        {{ topping.value }}
    ```

5. This appears to be every option even though we only selected Mushroons & Spinach, and it only got MUSHROOMS. To me this signifies that we are looping over the wrong contents; Instead of ```for topping_str in ToppingType:``` we should be looping over the toppings_list via ```for topping_str in toppings_list:```. Closer but not quite...

I belive this would be right if the toppings list propperly grabbed what we selected. To figure this out, I googled: ```flask get request only getting one selection on multiple objects``` and the first link was for this [stack overflow : Access Multiselect Form Field in Flask - Stack Overflowstackoverflow.com › questions › access-multiselect-for...](https://stackoverflow.com/questions/12502646/access-multiselect-form-field-in-flask) saying to change the ```.get``` to ```.getlsit```, and sure enough thanks to falsk auto refresh and it being a short form we now are seeing all the correct outputs on our debubg prints, but we're not done yet...
  
Dunt Dunt Duntaaaaa ... We still have to make sure it add the toppings to the pizza correctly and then adds the pizza to the database.

Now uncooment line 89 & 91 ```pizza.toppings.append(PizzaTopping(topping=topping_str))``` & ```db.session.add(pizza)``` and test again.

Back to 1: Creation Issues
TypeError: 'topping' is an invalid keyword argument for PizzaTopping

Change ```pizza.toppings.append(PizzaTopping(topping=topping_str))``` to \
```pizza.toppings.append(PizzaTopping(topping_type=topping_str))``` and add ```db.session.commit()```

Click Here For A More Verbose Walkthrough of our [Debuggin Methods](./exercise-1/solutions.md)

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

To debug this exercise, open a terminal `cmd + j` and navigate to the `exercise-3` folder, then run:

```zsh
python3 main.py
```

Ran the program, notied ```main.py``` only makes calls to the helper functions in ```untils.py``` and then prints the outputs thus we will be focusing out efforts there. Next looking at the trace back we look for the lowest line number as this is most likely our culprit. Then we continue from there.

1. ```Line 37``` in ```utils.py``` got an ```Index out of bounds error```, simply add ```-1```, makig the staement ```arr[k] = right_side[i-1]```
2. The indicies of an array can't be a float, to solve this issue lets type cast our equaton on ```line 48``` from ```mid = (high + low) / 2``` to ```mid = int((high + low) / 2)```
