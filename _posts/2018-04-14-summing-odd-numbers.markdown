---
layout: post
title:  "Summing Odd Numbers"
date:   2018-04-15 22:42:40 -0700
categories: Python
---



### Summing Odd Numbers
```python
def sum_odd_numbers(a, b):
    current_total = 0
    while(a <= b):
        print("a is currently: " + str(a))
        if a % 2 == 1:
            current_total = current_total + a
            print(str(a) + " is an odd number!")
        a = a + 1
    print("Sum of odd numbers between " + str(a) + " and " + str(b))
    print("Is equal to: " + str(current_total))
a = 4305
b = 8525
sum_odd_numbers(a, b)
```

### Working with Files
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

### Building a Dictionary
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
