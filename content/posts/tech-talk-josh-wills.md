---
title: Josh Wills - The Life of a Data Scientist
date: 2016-09-29
---

[![IMAGE ALT TEXT](http://img.youtube.com/vi/h9vQIPfe2uU/0.jpg)](https://www.youtube.com/watch?v=h9vQIPfe2uU "Airbnb Tech Talk: Josh Wills - The Life of a Data Scientist")

### Traits of Data scientist

##### Being relentless in a lazy way

Most of your model assumptions are incorrect. He mentions 2/3 of his ideas failed. Being lazy means you DO move on to the next idea and don't stick to it.

##### Humility

Being at best competent as a statician and  scientist. You know enough to talk to expert but you're not an expert but this allows you to learn.

### Math vs. Computer Science

Need to be good at both. Best to atleast study one of these and otherwise study science. Just studying Science (biology, neuroscience, ..) will give you the tools like relentlessness. 

Big Oh notation is important as it gives you the implications of runtimes of programs

Know your data structures

Computer science has algorithms and data structures, Data science has random variables and probably modeling

The difficulty is to find the context when none is provided. Give someone a challenge and mention that they should use a Hashmap. Chances are they won't have a problem implementing it. Give someone a challenge without any context (don't mention hashmap) and now you have a proper indication of a real-world response.

Statisticians typically don't have the computer science habits. Modular software, testing, code reviews, continuous integration, source control, ..

### Kaggle competitions

Kaggle skips a lot of steps. A lot of the work has been done for you. Implementing the machine learning part is typically one of the last steps.

### Hadoop & data science

If the traditional infrastructure isn't sufficient, a scientist will find a way to get it to run. It's part of the job. 

#### Unit of analysis problem

Relational databases are bad at:

* COUNT DISTINCT - Star models are not optimized for this 
* Cursors - If you are using cursors, there is something wrong
* ALTER TABLE_OF_DOOM - That one table in your data warehouse that you cannot touch

Databases are optimized to analyse transactions. Financial reporting, enterprise resource planning, ... 

Asking questions where all the things you need to know are not in a single table row is typically unperformant in a database.

Hadoop is simply a file system. You can structure your data as you like. Pull all the fields you need into a single record.

### Where should you work when starting out

Start up - Wearing two hats, jack of all trades.

Close to the money - You can convince people how much money you save or make the company. 

### Education and growth

Data scientists usually work in lonely teams, by themselves. No contact and no sharing of data because it's too valuable. No sharing of best practices. Need for communities.

### Realtime ML 

Realtime ML is rarely necessary. Pattern in data doesn't change so fast.

Sometimes writing code to test 'how something will turn out' takes longer than implementing an experiment on live users and seeing the result.

### Valuable stats content to learn

* Linaer Regression
* T Test 
* Binominal distributions
* Confidence intervals

### Josh Wills

Funny and down to earth guy. And I like that he's wearing sandals :) 
