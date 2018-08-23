---
layout: post
title:  "The Modulo Operator, Files, and Dictionaries"
date:   2018-04-15 22:42:40 -0700
categories: Python
---
### The Modulo Operator

The modulo operator symbol is '%' in Python and the syntax for it's use is NUMBER_1 % NUMBER_2. This operator returns the remainder of dividing NUMBER_1 by NUMBER_2. Often times, the first time that you'll need to use the modulo operator is when you want to determine if a number is even or odd.

The modulo 2 (NUMBER % 2) of an odd number will always have a remainder while the modulo 2 (NUMBER % 2) of an even number will not. The function below is a good programmatic representation of this idea; it builds the sum of all of the odd numbers from argument 'a' to argument 'b'.

```python
def sum_odd_numbers(a, b):
    current_total = 0
    while(a <= b):
        print("a is currently: " + str(a))
        if a % 2 != 0:
            current_total = current_total + a
            print(str(a) + " is an odd number!")
        a = a + 1
    print("Sum of odd numbers between " + str(a) + " and " + str(b))
    print("Is equal to: " + str(current_total))
a = 4305
b = 8525
sum_odd_numbers(a, b)
```

You can see the usage of the modulo operator on line 5 of the program. 'a % 2' will not be equal to 0 (will not have a remainder) whenever a is odd. When that if returns true, it will sum the total of the previous odd numbers with the current 'a'. You can see that this program will run from the start at 'a' until to end at 'b'.  

### Working with Files

Working with files is an essential part of any complex Python work. You open a file with the 'open' function. Be sure to specify how that file should be read; in the program below I use 'r' to specify read only and 'w' to specify read and write. This program reads in a file, and then creates a new file with just the even lines of the initial file.
```python
f = open ('working_with_files_text.txt', 'r')
output = open('output.txt', 'w')
line_number = 1
for line in f:
    print("Current line number: " + str(line_number) + " and line: ")
    if line_number % 2 == 0:
        print("Even line!")
        output.write(line + '\n')
    print line
    line_number = line_number + 1
output.close()
f.close()
```
I haven't talked about for loops yet, so I'd like to explain how the above one works. The 'line' in 'for line in f' doesn't exist in the program until it is run; 'line', in this case, is just the name for the current loop of for. The 'f' does exist as it is the name of the file that was opened at the start of the program.

Again, you'll see usage of the modulo operator here. This time I'm using it to select just the even numbered lines. To recap, NUMBER % == 0 will hold true for even numbers and NUMBER % != 0 will hold true for odd numbers. I'd also like to point out that I use the .write function, called on the 'output' file object, to write each of the previously-selected even-numbered lines. And finally, remember to run .close() on each of your file objects once you are done.

### Building a Dictionary

The program that I'm about to talk about uses a dictionary to count the number of times a word occurs in a given string. file.readline() reads *only one* line. I'm using in this case because there's only one line. I'd use .readlines() if there were multiple lines. The lines are split on spaces (the default of .split()) and then I use a for loop to cycle through all of the individual words.

```python
file = open('rosalind_ini6.txt', 'r')
output = open('rosalind_ini6_output.txt', 'w')
dictionary = {}
line = file.readline()
# print(line)
# There is no punctuation (only spaces), so I can split on ' '
# print(line.split())
split_line = line.split()
for word in split_line:
    #print(word)
    if word in dictionary:
        dictionary[word] = dictionary[word] + 1
    else:
        dictionary[word] = 1

# print(dictionary)
for item in dictionary:
    # print(item + ' ' + str(dictionary[item]))
    output.write(item + ' ' + str(dictionary[item]) + '\n')
file.close()
output.close()
```
I create a dictionary on line 3 of the program with 'dictionary = {}'. The syntax of adding to a dictionary is DICTIONARY[DICTIONARY_KEY] = DICTIONARY_ENTRY. Note the usage of if and else here. I check if the current word (from the or loop) is 'in' the dictionary and, if it is, then the entry for the dictionary is bumped up by 1. Otherwise, the dictionary entry for that item is created with an entry of 1.
