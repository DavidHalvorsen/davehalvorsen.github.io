---
layout: post
title:  "Python Functions and List Slicing"
date:   2018-04-14 22:42:40 -0700
categories: Python
---
### Strings and Lists
Let's talk about some basic Python functions in the context of simple exercises! Say that you had some text that you wanted to cut up and combine ... For example, you might want to pick two slices of a text string and connect them. This function takes 5 arguments: an inputted text string, a starting slice for side a, an ending slice for slice a, a starting slice for side b, and an ending slice for side b. The slices of side a and side b are then combined.

```python
def slice_and_dice(text_string, a, b, c, d):
    text_string_ab_slice = text_string[a:b+1]
    text_string_cd_slice = text_string[c:d+1]
    left_space_right_slices = text_string_ab_slice + ' ' + text_string_cd_slice
    return left_space_right_slices
# I tested the code w/ this stuff:
# text = "HumptyDumptysatonawallHumptyDumptyhadagreatfallAlltheKingshorsesandalltheKings \ menCouldntputHumptyDumptyinhisplaceagain."
# print(slice_and_dice(text, 22, 27, 97, 102))

text = "vQj40bDqlDzbiEMUobkQ01senjgnUhrxilwiuGrOvisxF7KqgJ7TJbzmwXyaHgdtvqRBiLfWUF9CtI7\
kMBWwGyxYVfk0rwdZSM3kSDT0hpzfiber73j3R5WgtTrfoIuowfuFq6Za7JQtg8bvug6NdRXxGi27Yks\
MEe6g1vfqyyxBoxxOTWEPMbbFHYNmprubaSPNL."
print(slice_and_dice(text, 39, 42, 107, 111))
```

First of all, a Python function is a callable set of Python code of the format: def FUNCTION_NAME(FUNCTION, INPUTS): INDENTED CODE. Python functions don't have curly brackets enclosing the code the same way that R does. In Python, the indentation is the only thing that matters, so it's important to be very careful with it. Don't use spaces! Use tabs! Tabs are a quick and repeatable distance.

As you can see in the 'slice_and_dice' function definition below, function arguments are enclosed within a set of parenthesis and separated by commas. These are the name placeholders for the functional arguments submitted to the function. Check out the call to this function down at the end of the code block. The call looks a lot like the functional definition except that the call has the actual inputs. Note that 'text' is a variable that is defined above the call to the function.

Pound signs (#) are used for in-line comments. If you're just recently learning to code, you'll be surprised how much you forgot about why functions were defined it certain ways, so it's very important to carefully explain yourself. I'm being a hypocrite in the function call below because I'm only using pound signs to talk about how I tested the code, but in my defense, this is an easy program. You'll see plenty of comments in my more complicated code.

I'm sure you can guess what 'print' does, haha. I'm using it here to print an output to the screen. Alternatively, you could print output to a file. That's something that I'll be explaining later. Looking at the indented bit of code within the function, you'll see the use of square brackets; those are used to 'slice' the text. 'text_string', one of the functional arguments, will be sliced with a starting point of argument 'a'. The reason that the end slice position, in the bracket, isn't just 'b' is because Python list slice ends are *not* inclusive; that's why there's a +1.

The variable 'left_space_right_slices' is the concatenation of the 'text_string_ab_slice' and the 'text_string_cd_slice'. This is done with a plus sign. I've used a ' ' (blank space) to create a gap between the left side and the right side. Finally, the output of the function is returned. It's a simple function, but I did enjoy reviewing it again. I believe it is important to go back to basics to strengthen conceptual understanding.
