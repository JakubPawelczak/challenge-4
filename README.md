# Challenge 4 - Dialogs

**Congratulations on completing the third challenge!**

In this exercise we will teach Bixby to talk like we want him to!

1. Download the capsule code for this challenge.

2. Look around, get familiar with the capsule - Startup Search!

3. Launch the simulator

4. Click on compile!

3. Write the sentence: **what is the golden standard**. Click **Run NL**

4. Bixby found something, great... well... not quite.
We already see that it found a result we don't need Bixby to say that.
Let's think of a way to make Bixby say something cooler.

5. Jump to code/startups.js -> there you can find our mockup database of startups!

6. Each startup contains a few values: 

| GoldenStandard | |
| ------:| -----------:|
| name | The Golden Standard |
| desc | When it comes to gold, we know where to find it |
| url | /goldenstandard.jpg |

How about teaching Bixby to say the name of the startup he found and read the description right away?

7. For that we need a **Dialog**

8. Let's create the file: Go to _resources/en/dialogs_ -> _right click_ ->  _new_ -> _Dialog_
Let's call it _StartupResult_ to know right away what we're using it for.
We will keep all the setup fields as default, feel free to ask one of us what are they for.
You can delete the file _.gitkeep_ it was there to have the folder on github.

9. Great we have a new file with something written in it already, let's analise it.

```
dialog (Result) {
  match: __MATCH_PATTERN__
  template("__TEMPLATE_TEXT__")
}
```

10. **dialog (Result)** this defines a dialog based on a result. What _result_?

11. That's what we define in **match: __MATCH_PATTERN__**
Here we need to match our newly create dialog to a certain model. Well we called our file _StartupResult_ so the model we want our dialog to match is _Startup_! What is the Startup model? 

12. Go to models/concepts/structures/Startup.model.bxb and see for yourself!
Try to match the fields of this _structure_ to our database of startups (code/startups.js)
Feel free to ask if you wnat more explanations.

13. Once we know what we want to match our dialog to, let's write that in:

```
match: Startup
```

14. We will want to access the fields in our structure so we will add a name to ease our coding later.
let's add **(this)** after _match: Startup_

```
match: Startup (this)
```

15. Now on to the fun part!
we have an empty template: _template("__TEMPLATE_TEXT__")_
Write anything you want in the place of *__TEMPLATE_TEXT__*
I want Bixby to rule the world so I wrote this:

```
template("I am the king of the world!")
```

16. Launch the simulator
Write the sentence: **what is the golden standard**.
Click **Run NL**

17. So did Bixby say what you've taught it?
Cool, right?
Now jokes aside, let's make it read the name of the startup it found and read the description as well
for that we will access values from our _Result Structure Startup_ 
In the Bixby meta coding language we write it like this:

```
template("#{value(__VALUE_TO_BE_ACCESSED__)}")
```

First we want to access the name of the startup.
Change *__VALUE_TO_BE_ACCESSED__* to this.name (go to point **14** for the explanation why we write "this.")
By now your template should look like this:

```
template("#{value(this.name)}")
```

18. Try out how it works in the simulator!

19. And now add  three dots after the name to make a little pause (...)
then add one more value which will be the description of the startup from our database

> first HINT: Any time you change something in the template (between the template braccets -> template("HERE") )
> run the simulator to check how it affects what Bixby says
>
> second HINT: fill in the blanks

```
template("#{value(this.name)}BLANK#{value(BLANK)}")
```

20. It's time for the final test of this challenge!
Go to the simulator and write a question about a startup that is not in our database
I asked: _what is the little company_ I'm pretty sure it's not in the database
The generic Bixby answer is alright but we want to customize it.
Create a new _Dialog_ file like in point **8.**
Call it _StartupNoResult.dialog.bxb_

21. change the dialog type to _(NoReult)_

22. Match it the same way we matched our first dialog (like in points **13** and **14**).

23. Customize your template (like in point **15**).

24. Run the simulator and show us how you just taught Bixby to speak!
