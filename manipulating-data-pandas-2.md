---
title: Pandas 2
layout: post
weight: 10
hidden: true
---
​
Pandas 2 Lesson Plan
===
​
​
**Course**: Data Science   <br/>
**Mod**: Module 1                    <br/>
**Topic**: Pandas 2  <br/>
**Amount of time**: 1.5 hours <br/>
**Author**: Rachel Hirsch, Greg , Alison Peebles Madigan
​
​
***
​

​
## Lesson Summary:

# Note: most current version of steps is in student notebook.
​
#### Topic:
Pandas 2
#### Learn.co material:
(link to github)
#### Prerequisite knowledge/ Prework:
Learn.co README files
#### Learning goals for this lesson:
SWABT:

Use the pandas library to:

- Get summary info about a dataset and its variables
  - Apply and use info, describe and dtypes
  - Use mean, min, max, and value_counts 
- Use apply and applymap to transform columns and create new values
- Explain lambda functions and use them to use an apply on a DataFrame
- Explain what a groupby object is and split a DataFrame using a groupby
- Reshape a DataFrame using joins, merges, pivoting, stacking, and melting



#### Misconceptions:
(none filled out)

#### Materials
- Data set (https://data.austintexas.gov/Health-and-Community-Services/Austin-Animal-Center-Outcomes/9t4d-g238/data)
- Student jupyter notebook files (link here)
- answer code for more complex data cleaning at the bottom

***

## Lesson Outline:

**Step**: Introduction and outline of lesson <br/>
**Time**: 5 min

_Goal/Scenario:_<br/>
You have decided that you want to start your own animal shelter, but you want to get an idea of what that will entail and get more information about planning. In this lecture, we are continue to look at a real data set collected by Austin Animal Center over several years and use our pandas skills from the last lecture and learn some new ones in order to explore this data further.

_Learning Goals in sequence:_<br/>
- Get summary info about a dataset and its variables
  - Apply and use info, describe and dtypes
  - Use mean, min, max, and value_counts 
- Change data:
  - Use apply and applymap to transform columns and create new values
  - Explain lambda functions and use them to use an apply on a DataFrame
- Reorganize data:
  - Explain what a groupby object is and split a DataFrame using a groupby
- Reshape data:
  - Reshape a DataFrame using joins, merges, pivoting, stacking, and melting

**Step**: Activation <br/>
**Time**: 10 min

Discussion prompts:
- Let's take a moment to examine the data set. What kinds of questions can we ask this data and what kinds of information can we get back?
- Write down the ideas students come up with and supply some other suggestions. Try to generate enough suggestions for each pair to have a question to work on.


**Step**: Learning Goal 1: _Summarize data_ <br/>
**Time**: 14min

_Demonstrate_: 5 min <br/>
Show and use the df.describe() and df.info() summary statistics methods
- Use `heart.csv` dataset to demonstrate exploring a dataset using `head()`, `columns`, `shape`, `info()`, `describe()`, and `dtypes`.

Discuss and introduce examples of built-in Pandas methods for calculating summary statistics (.mean(), .std(), .count(), .sum(), .mode(), .median(), .std(), .var() and .quantile())
- Again, use `heart.csv` to practice `mean`, `min`, `max`, `sum` and `value_counts`

- Small check together of understanding how to use this code on resteg

_Application_: 8 min <br/>
Students look to apply those functions to analysing the animal shelter dataset

_Informal assessment_: 1 min <br/>
"Quick fist of five check, how confident are we that we can utilize the Pandas library statistics functions on our data sets and apply functions to pandas objects? zero is not at all. five is ready to go."
- follow up with students who do not feel confident

- Use apply and applymap to change all values in a series/dataframe to strings

**Step**: Learning Goal 2:  _Change data_ <br/>
**Time**: 14min

_Demonstrate_ :
- lead students through using `applymap`, `map`, and `lambda` on uci data

_Application_: 8 min <br/>
Students look to apply those functions to analysing the animal shelter dataset
- update dates to datetime
- convert age to floats

_Informal assessment_: 1 min <br/>
 To assessment check

**Step**: Learning Goal 3: _Reorganize Data_ <br/>
**Time**: 13 min

_Demonstrate_: 7 min <br/>
- Discuss what a groupby object is and how it can be used
- Show how to use a groupby to manipulate a DataFrame on UCI

_Application_: 5 min <br/>
- Students will apply a groupby split on the animal shelter data in their pairs

_Informal assessment_: 1 min <br/>
"Thumbs up, down, or middle on groupby objects."
- follow up with any non-thumbs up responses

**Step** 3:  _Reshape a DataFrame_ <br/>
**Time**: 9 min

_Demonstrate_: 3 min <br/>
Using the UCI data:
- Discuss joins and merges
- Show how to join and merge
- Discuss pivoting, stacking, and melting
- Show how to pivot, stack, and melt

_Application_: 5 min <br/>
they repeat what is done on UCI

**Step**: Integration: _Detect, replace and drop missing data using Pandas_ <br/>
**Time**: 14 min

_Demonstrate_: 6 min <br/>
- Discuss all steps needed to get to final goal.

_Application_: 7 min <br/>
Join the data from the Austin Animal Shelter Intake dataset to the outcomes dataset by Animal ID.

Use the dates from each dataset to see how long animals spend in the shelter. Does it differ by time of year? By outcome?

The Url for the Intake Dataset is here: https://data.austintexas.gov/api/views/wter-evkm/rows.csv?accessType=DOWNLOAD

Hints :

- import and clean the intake dataset first
- use apply/applymap/lambda to change the variables to their proper format in the intake data
- rename the columns in the intake dataset before joining
- join data sets
- create a new days-in-shelter variable

Use group_by to get some interesting information about the dataset
Make sure to export and save your cleaned dataset. We will use it in a later lecture!

use the notation df.to_csv() to write the df to a csv. Read more about the to_csv() documentation here

**Step**: Assessment:  <br/>
**Time**: 10 min<br/>
- quick quiz!!!

**Step**: Reflection:  <br/>
**Time**: 7 min <br/>
- "What was one thing that you found challenging, one thing that surprised you, and one thing you found interesting?"



Answer code for processing data:

```

animal_outcomes = pd.read_csv('https://data.austintexas.gov/api/views/9t4d-g238/rows.csv?accessType=DOWNLOAD')

animal_outcomes.columns
new_names = ['id', 'name', 'date', 'monthyear', 'dob', 'outcome', 'outcome_s', 'animal', 'sex', 'age', 'breed', 'color']

animal_outcomes.columns = new_names

animal_outcomes.dtypes

# method one - not worth it
test_ages = animal_outcomes['age'].str.split(" ", n = 1, expand = True) 
animal_outcomes['age_num'] = test_ages[0]
animal_outcomes['age_var'] = test_ages[1]

# method 2 - what we will do 
animal_outcomes.drop(columns = ['age'], inplace = True)
animal_outcomes.head()

animal_outcomes['date']=animal_outcomes['date'].map(lambda x: x[:10])
animal_outcomes['date'] =  pd.to_datetime(animal_outcomes['date'], format='%m/%d/%Y', errors = 'ignore')

animal_outcomes['dob'] =  pd.to_datetime(animal_outcomes['dob'], format='%m/%d/%Y', errors = 'ignore')

animal_outcomes['age_in_days'] = (animal_outcomes['date'] - animal_outcomes['dob'])
animal_outcomes['years'] = animal_outcomes['age_in_days'].map(lambda x: x.days/365)

```