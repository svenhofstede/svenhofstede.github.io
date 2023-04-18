---
title: Predicting titanic survivors
date: 2016-10-21
---

## Predicting Titanic Survivors.. again

Yes.. I also decided to give the Titanic survival prediction a go. It's probably the go-to starting point for people wanting to learn Machine Learning. Apart from some missing values the dataset itself is pretty clean, the label we are trying to predict 'makes sense'. You can easily reason about what we are going for. If you've watched the movie you will also have a good idea about what features might be useful ( *Woman and children first!* ).

## The Code

```python
%matplotlib inline

import pandas as pd
import numpy as np
import math
import csv as csv
from sklearn.ensemble import RandomForestClassifier
import re
import matplotlib.pyplot as plt
```


```python
train_df = pd.read_csv('train.csv', header=0)
```

### Length of the names
Tried length of the name. My thinking was: Richer people tend to have longer, more fancy names. But the model did not improve much at all.


```python
# train_df['Len'] = train_df['Name'].map(lambda x: len(x))
```

Creating a new field called Gender to preserve the Sex field.


```python
train_df['Gender'] = train_df['Sex'].map( {'female': 0, 'male': 1} ).astype(int)
```

### Cleaning up the Embarked column

The IF statement just checks if there are any NULL values in the Embarked column. After that it fills in the empty entries (NULL) of the Embarked column with the most occurring value (Mode). Once those gaps are filled in I create a distinct list of the possible values of the Embarked column and store those in `Ports`. Then I create a dict to store these distinct values and use the dict to convert the Embarked strings to their corresponding int value in the dict. 


```python
if len(train_df.Embarked[ train_df.Embarked.isnull() ]) > 0:
    train_df.loc[train_df.Embarked.isnull(),'Embarked'] = train_df.Embarked.dropna().mode().values

Ports = list(enumerate(np.unique(train_df['Embarked'])))    # determine all values of Embarked,

Ports_dict = {name : i for i, name in Ports}
train_df.Embarked = train_df.Embarked.map( lambda x: Ports_dict[x]).astype(int)     # Convert all Embark strings to int
```

### Add Title field

It read somewhere online that someone's title can contain interesting information. Not only for improving the model directly but also for 'forecasting' the passengers age. Certain titles are only given to people of a certain age group. *Master* for example is given to a young boy. Another example is the difference between Mrs and Ms. 

I'm also converting the string value of the title to an integer. 


```python
names_to_keep = ['Miss','Mr','Mrs','Ms','Master']

def getTitle(name):
    title = re.search(', ([A-Za-z]+).', name).group(1)
    
    if title in names_to_keep:
        return title
    else:
        return 'Others'
  
train_df['Titles'] = train_df.Name.map( lambda x: getTitle(x))

Titles = list(enumerate(np.unique(train_df['Titles'])))
Titles_dict = {name : i for i, name in Titles}

train_df['TitlesNum'] = train_df.Titles.map( lambda x: Titles_dict[x]).astype(int)
```

...and now fill in the empty ages with the median of title group


```python
mean_ages = train_df.groupby('Titles')['Age'].mean().to_dict()
train_df.loc[train_df.Age.isnull(),'Age'] = train_df.Titles.map( lambda x: mean_ages[x] )
```

### Reading in test data


```python
test_df = pd.read_csv('test.csv', header=0)

# Create Gender column
test_df['Gender'] = test_df['Sex'].map( {'female': 0, 'male': 1} ).astype(int)

# Fix Embarked column
if len(test_df.Embarked[ test_df.Embarked.isnull() ]) > 0:
    test_df.Embarked[ test_df.Embarked.isnull() ] = test_df.Embarked.dropna().mode().values

Ports = list(enumerate(np.unique(test_df['Embarked'])))    # determine all values of Embarked,
Ports_dict = {name : i for i, name in Ports}    

test_df.Embarked = test_df.Embarked.map( lambda x: Ports_dict[x]).astype(int)


# Add Titles column
test_df['Titles'] = test_df.Name.map( lambda x: getTitle(x))
test_df['TitlesNum'] = test_df.Titles.map( lambda x: Titles_dict[x]).astype(int)


# Fix Age by adding median of title group 
mean_ages = test_df.groupby('Titles')['Age'].mean().to_dict()

for key, value in mean_ages.iteritems():
    if math.isnan(value):
        mean_ages[key] = test_df.Age.mean()

test_df.loc[test_df.Age.isnull(),'Age'] = test_df.Titles.map( lambda x: mean_ages[x] )
```


```python
# The isnull check each time to make sure the column has values
if len(test_df.Fare[ test_df.Fare.isnull() ]) > 0:
    median_fare = np.zeros(3)
    for f in range(0,3):                                              # loop 0 to 2
        median_fare[f] = test_df[ test_df.Pclass == f+1 ]['Fare'].dropna().median()
        test_df.loc[ (test_df.Fare.isnull()) & (test_df.Pclass == f+1 ), 'Fare'] = median_fare[f]
```


```python
ids = test_df['PassengerId'].values
```


```python
test_df = test_df.drop(['Name','Sex', 'Ticket', 'Cabin', 'PassengerId','Titles'], axis=1) 
train_df = train_df.drop(['Name','Sex', 'Ticket', 'Cabin', 'PassengerId','Titles'], axis=1) 
```


```python
train_data = train_df.values
test_data = test_df.values
```


```python
print('Training...')
forest = RandomForestClassifier(n_estimators=100)
forest = forest.fit( train_data[0::,1::], train_data[0::,0] )
print('Trained')

print('Predicting...')
output = forest.predict(test_data).astype(int)
print('Predicted')
predictions_file = open("forest_prediction.csv",  'w')
open_file_object = csv.writer(predictions_file)

open_file_object.writerow(["PassengerId","Survived"])
open_file_object.writerows(zip(ids, output))

predictions_file.close()
print('Done.')
```

    Training...
    Trained
    Predicting...
    Predicted
    Done.
    

## The result

After submitting, this predictions came back with a Kaggle score of **0.73206**. Hurray! Unfortunatly an earlier attempt while strictly following a tutorial had a score of **0.77512** so I cannot call it an improvement. 

# Lessons

At one point I was struggling to update values in a dataframe. After trying out all kinds of solutions myself I eventually looked for some help online. I found a Slack channel and was helped promptly. My issue was the following: 

```python
train_df[train_df.Age.isnull()]['Age'] = train_df.Titles.map( lambda x: mean_ages[x] )

# I got the following error:
# A value is trying to be set on a copy of a slice from a DataFrame.
```

Turns out I was trying to update a copy instead of the original dataframe. Dataframes are sometimes slighly inconsistent when it comes to returning either copies or views. The people in the [Slack channel](https://pythondev.slack.com/messages/data_science/) suggested to the `.loc` function on the dataframe to create a view instead of a copy. This is how the code looks after applying this fix. 

```python
train_df.loc[train_df.Age.isnull(),'Age'] = train_df.Titles.map( lambda x: mean_ages[x] )
```


More information about this can be [found here](http://pandas.pydata.org/pandas-docs/stable/indexing.html)