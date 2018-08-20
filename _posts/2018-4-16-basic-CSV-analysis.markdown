---
layout: post
title:  "Some Basic CSV File Analysis"
date:   2018-04-16 22:42:40 -0700
categories: R
---
I was surprised when I first heard that the bulk of data analysis projects in R involves obtaining and cleaning data. I figured I'd be spending a lot of time creating graphs and doing statistics, but the old saying is true. Most of the time you spend in R is spent getting data into usable formats. I found a couple of interesting CSV files from [Human Genome Project Participant Surveys]. All I wanted to do was to compare the average heights of the men and women, but I found myself needing to do a ton of data cleaning first.

You can check out my [Git Repository for this project] if you'd like to. First things first, I needed to read in the Excel data files. It became complicated before I even got started because the CSV file with the heights was separate from the CSV file with genders, so I needed to read in the files separately. CSV files are called 'CSV' because they are comma-separated-values. That's why sep=",". Also, header=TRUE when the first rows are the column names.

```R
height_CSV <- read.csv(file="PGPBasicPhenotypesSurvey2015-20180819174645.csv", header=TRUE, sep=",")
gender_CSV <- read.csv(file="PGPParticipantSurvey-20180819174510.csv", header=TRUE, sep=",")
```
The variables height_CSV and gender_CSV, that I just created, contain the *ENTIRE* CSV files, so we'll need to cut them back significantly. You can do that with the '$' by selecting single columns. This code specifies just the Height column of the height_CSV and the Gender column of the gender_CSV. Both of these columns are in excess of 1,000 columns, so I've used list slicing, with the square brackets, to limit the range of the variables.
```R
height_CSV$Height[1:10]
gender_CSV$Gender[1:10]
```
I want to be able to compare the heights of men and women, so I need gender and height to be in a standardized format, so I started to look at the values. First I'll talk about height. It's supposed to be in the format of FEET'INCHES". However, looking through all of the values you'll find that there are a variety of formats.

```R
# stored the column as a variable for eas of typing
heights <- height_CSV$Height
# print out all heights is commented out because it's >1,000 lines
# heights
# here are my selection of the different height types:
heights[1]
# double single quotes instead of double quotes
heights[18]
# blank
heights[89]
# range of height
heights[796]
# triple single quotes
heights[918]
```
Here is the R output for the above code. You can see the regular FEET'INCHES" format, two single quotes at the end FEET'INCHES'', a blank entry, a range of height from 5'11" to 6'0", and triple single quotes at the end of the height. Obviously the heights here are of a variety of strange formats. I'll need to write a function that can make sense out of all of the weird formatting options. Check for a future article of mine on how I did that.
```console
[1] 6'2"
42 Levels:  4'10" 4'11" 4'8''' 5'0" 5'1'' 5'1" 5'10'' 5'10" 5'11'' ... 6'7"
[1] 5'6''
42 Levels:  4'10" 4'11" 4'8''' 5'0" 5'1'' 5'1" 5'10'' 5'10" 5'11'' ... 6'7"
[1]
42 Levels:  4'10" 4'11" 4'8''' 5'0" 5'1'' 5'1" 5'10'' 5'10" 5'11'' ... 6'7"
[1] 5'11" to 6'0"
42 Levels:  4'10" 4'11" 4'8''' 5'0" 5'1'' 5'1" 5'10'' 5'10" 5'11'' ... 6'7"
[1] 4'8'''
42 Levels:  4'10" 4'11" 4'8''' 5'0" 5'1'' 5'1" 5'10'' 5'10" 5'11'' ... 6'7"
```

[Human Genome Project Participant Surveys]:https://my.pgp-hms.org/google_surveys
[Git Repository for this project]:https://github.com/DaveHalvorsen/Personal_Genome_Project
