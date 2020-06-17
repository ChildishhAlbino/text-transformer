# Optimus
A Python Tool for transforming text into other forms. (Work in Progress!)

## Overview

As a notorious scripter, I want a more general way to transform text from the clipboard into various forms to make my life easier. For example:

If I get given a list like this:
```
grape
apple
banana
pineapple
```
and I want to make it into JSON fashion I would need to manually add the commas and the brackets and potentially want to remove the new lines.

That's a lot of manual work and if I have a large list of items like this it might take me a while.

So I propose I can do this instead
```
-> python optimus.py // i have copied the above text to my clipboard

You wish to transform:

----------
grape
apple
banana
pineapple
-----------

How would you like to transform it?
-> replace{'/n', ',/n'} : (for '/n' < 3) >> replace{'/n', ' '} >> surround{'[', ']'}

That would have the follow effect: 
[grape, apple, banana, pineapple]
```
### So  that's great, but what does that mean?

Ok let's break it down.

Firstly `>>` is how we separate steps into blocks. The result of one block is handled by the next. This allows us to do transformations in stages, providing more granular changes.

Secondly each block does a specific job. The first being the most complicated of the three.

`replace{'/n', ',/n'} : (for '/n' < 3)` = replaces all newline characters with a comma and a new line for the first 3 newlines

This is done to basically append a comma before the end of the first 3 lines (we don't want a comma on the last line)

`:` is used to denote a conditional transformation; of which the condition is specified in the brackets following. You can chain together conditions using `||` for logical OR or use `&&` for logical AND.

---

The next transformation does the same thing except without the condition. It replaces all the new lines with blank spaces so the list is now:
```
grape, apple, banana, pineapple
```

---

The last step `surround{'[', ']'}` is completely self explanatory. It takes a state and surrounds it with the characters provided. 