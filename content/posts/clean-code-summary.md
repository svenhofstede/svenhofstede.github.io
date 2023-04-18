---
title: What Clean Code taught me
date: 2016-12-12
---
*This blog post is work-in-progress while working myself through the book. It will loosely follow the structure of the book.*

I'm currently working on reading through Clean Code by Robert C. Martin. It was clear from the start that the book is full of incredible content and it's well worth the time to study it properly. I'm trying to capture the key take-aways I have come across. There is much more to the book then what I'm highlighting here but these are things that were somewhat new to me and stuck in my mind as being worth remembering. I would suggest any programmer to have a look at this book in full. 

I'm approaching this book from an un-experienced programming in terms of application development. Most of the concepts/patterns are new to me.

## The Art of Naming

*There are two hard things in computer science: cache invalidation, **naming things**.*

The naming of variables and functions is an art in itself. You need to come up with a name that perfectly explains why and how a variable or function is used and what it is. It can't be too long but it shouldn't be too short. Longer is better then shorter if that means the intent is made more clear. 

#### Make it Searchable

If possible, make sure the name is searchable. You need to be able to easily jump to a variables. Don't call them `x`, `counter` or `max_number`. If you are using `counter` once, you'll probably use it often so finding the right one with your editor find tool is inconvenient. And you don't want the search to bring you to every `x` in the text. 

#### Talking about variables

Make stuff pronounceable. This helps greatly in talking about the functions and variables with other people. Instead of having to refer to `df_incr` we can just **say** `dataframe_incremental`. Yes it might be longer to type but copy-paste and auto-complete are commonplace.

#### Stick to a word per concept

Agree and stick to a single word for a single concept. Are you *fetching* or are you *getting* a record? Decide and use this going forward when necessary. Don't mix `get_record_by_id` with `fetch_records`.

## Functions

#### Reduce complexity

Functions should do one thing. 

For readability you want to limit the number of indent levels to 1 or 2. Anything more then 2 probably means your function is doing *too much*. Functions should have **at most** 3 arguments but ideally you should be aiming for zero if at all possible. Increasing the number of arguments will:

* Hard to understand what the function does. 
* They pollute the simplicity of the API
* It makes testing more complex 
 
If you notice your functions really needs multiple argument, consider if it makes sense to replace them by an input object instead.

#### Avoid side effects

> In computer science, a function or expression is said to have a side effect if it modifies some state or has an observable interaction with calling functions or the outside world.

Side-effects are lies. Your function is doing something that isn't advertised in the name. They also make it difficult to test your function as you need to set-up the *outside world* for your function to work. Pure functions are much more reliable as they are guaranteed to return the same value for a given input.  

#### Extract try-catch blocks. 

By writing your code in a try block you are mixing error processing with the actual processing.


```python
try:
  i = 1
  i = do_something_to_variable(i)

  do_something()
  do_another_thing()
except:
  raise
```  

Instead pull this out into a seperate function.

```python
def do_loads_of_things():
  i = 1
  i = do_something_to_variable(i)

  do_something()
  do_another_thing()

try:
  do_loads_of_things()
except:
  raise
```

#### Write test, write code, refactor

It's hard to write clean functions on first pass and people rarely do. There is nothing wrong with writing ugly code that just works and then refactoring it to make it clean. Remember to write tests first so you can safely refactor your code.

## Comments

Comments, in general, should be avoided. Try to replace with more expressive function names. 

Don't leave commented code hanging around. If you don't need it, get rid of it.  If someone (or even yourself) comes along at a later date they don't know why the code is commented out. They would fear either removing or uncommenting it. Remember you have source control to retrieve old code. Same thing for journal comments, this is dealt with by the source control. No need to track this in the code.

Add comments near the source of the thing you are commenting. Don't add a comment for a function where you are using the function. Instead comment where the function is defined.

## Objects and Data Structures

#### The difference

The difference between objects and data structures lies in their usage. Data structures are meant to provide access to the data directly. Objects hide direct access to data but expose behaviours. They abstract away the retrieval of data.

You should not be able to navigate through objects by chaining as the underlying implementation should be hidden from sight. 

## Error Handling

Don't forget to write tests for errors that you expect to have happen. Make sure these are tested as well.

Add context to the error message. When catching the error you are normally aware of why this error is being thrown. Convey this knowledge in the error message so that, when the error occurs, you can easily recall it. 

Wrap third party API exceptions with your own single error. This way you don't need to handle all the possible errors every time you use the API.

## Boundaries

When dealing with third party API and the boundaries between it and your application, write tests for this boundary. Write tests to learn how the API works. These tests can be simply calling the API and not getting an error. This would be a successfull test. This has two advantages:

* It's a great way to learn the API
* Failing tests will alert you of changes in the API (after a new release for example)

#### Adapter pattern

The Person objects has a make_noise() but Dog doesn't. It only has bark(). We implement a DogAdapter which defines the make_noise() to call bark(). All other functions of Dog are routed to the Dog object itself using the __getattr__. This 'catch-all' sends all remaining function calls to the underlying Dog object.

```python

from dog import Dog
class Person(object):
    """A representation of a person in 2D Land"""
    def __init__(self, name):
        self.name = name

    def make_noise(self):
        return "hello"

class DogAdapter(object):
    """Adapts the Dog class through encapsulation"""
    def __init__(self, canine):
        self.canine = canine

    def make_noise(self):
        """This is the only method that's adapted"""
        return self.canine.bark()

    def __getattr__(self, attr):
        """Everything else is delegated to the object"""
        return getattr(self.canine, attr)

def click_creature(creature):
    """
    React to a click by showing the creature's
    name and what is says
    """

    return (creature.name, creature.make_noise())

```

## Unit Tests

Unit tests are as important as the production code itself. They not only make sure your program works as you intended it to but also allows for safe refactoring. Refactoring without tests is a gamble. 

The 5 FIRST principles of testing:

* Run **F**ast
* **I**ndependant from other tests
* **R**epeatable
* The outcome is **S**elf-validating. Outcome is binary.
* Written **T**imely so before the production code