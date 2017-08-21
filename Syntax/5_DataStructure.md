# Data Structures

## List Methods

method           | description             | note
-----------------|-------------------------|---------
 list.append(x)        | add a item to the end   | a[len(a:)] = [x]
 list.extend(iterable) | append all items to the end | a[len(a):] = iterable
 list.insert(i, x)     | the first argument is the index of the element before which to insert| a.insert(len(a), x) = a.append(x)
 list.remove(x)         | It's an error if there is no such item|
 list.pop([i])          | remove the item at the given position and return it. If no index is specified, a pop() removes and return the last item in the list. | 
 list.clear()           |  remove  all the items | del a[:]
 list.index(x[, start[, end]]) | return zero-based in the list of the first item whose value is x. Raises a ValueError if there is no such item. The returned index is computed relative to the beginning of the full sequence rather than the start argument
 list.count(x)          | return the number of times x appears in the list|
 list.sort(key=None, reverse=False) | Sort the items of the list in place. Arguments see [sorted()](https://docs.python.org/3/library/functions.html#sorted)|
 list.reverse()         | reverse the elements of the list in place.|
 list.copy()            |  return a shallow copy of the list.   | a[:]


 ``` Python
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.count('apple')
2
>>> fruits.count('tangerine')
0
>>> fruits.index('banana')
3
>>> fruits.index('banana', 4)       # Find next banana starting a position 4
6
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
>>> fruits.append('grape')
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
>>> fruits.pop()
'pear'
 ```

## List => Stack
* list.append()
* list.pop

``` Python
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]
```

##　List => Queue
* list.append()
* list.pop(0)

**Note**: _lists are not efficient for this purpose. While appends and pops from the end of list are fast, doing inserts or pops from the beginning of a list is slow (because all of the other lements have to be shifted by one)._ 

To implement a queue, use collections.deque which was designed to have fast appends and pops from both ends. For example:

``` Python
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")
>>> queue.append("Graham")
>>> queue.popleft()
'Eric'
>>> queue.popleft()
'John'
>>> queue
deque(['Michael','Terry', 'Graham'])
```

## List Comprehensions

A list comprehension consistes of  brackets containing an expression followed by a `for` clause, then zero or more `for` or `if` clauses. The result will be a new list resulting from evaluating he expresion in the context of the `for` and `if` clauses which follow it.

**Note:** _if the expression is a tuple(e.g. the `(x, y)`) in the previous example), it must be a parenthesized._

### Example 1:
```
>>> squares = []
>>> for x in range(10):
...     squares.append(x**2)
...
>>> squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```
equivalently:

``` Python
squares = list(map(lambda x: x**2, range(10)))
```

or 

``` Python
squares = [x**2 for x in range(10)]
```

### Example 2:

``` python
>>> combs = []
>>> for x in [1,2,3]:
...     for y in [3,1,4]:
...         if x != y:
...             combs.append((x, y))
...
>>> combs
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

equals:

``` python
>>> [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

### Example 3:

``` python
>>> vec = [-4, -2, 0, 2, 4]
>>> # create a new list with the values doubles
>>> [x*2 for x in vec]
[-8, -4, 0, 4, 8]
>>> # filter the list to exclude negative numberss
>>> [x for x in vec if x >= 0]
[0, 2, 4]
>>> # apply a function to all the elements
>>> [abs(x) for  x in vec]
[4, 2, 0, 2, 4]
>>> # call a method on each element
>>> freshfruit = ['  banana', ' loganberry ', '   passion fruit']
>>> [weapon.strip() for weapon in freshfruit]
['banana', 'loganberry', 'passion fruit']
>>> # create a list of 2-tuples like (number, square)
>>> [(x, x**2) for x in range(6)]
[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
>>> # the tuple must be parenthesized, otherwise an error is raised
>>> [x, x**2 for x in range(6)]
  File "<stdin>", line 1, in <module>
    [x, x**2 for x in range(6)]
               ^
SyntaxError: invalid syntax
>>> # flatten a list using a listcomp with two 'for'
>>> vec = [[1,2,3], [4,5,6], [7,8,9]]
>>> [num for elem in vec for num in elem]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Example 4: 

``` python
>>> from math import pi
>>> [str(round(pi, i)) for i in range(1, 6)]
['3.1', '3.14', '3.142', '3.1416', '3.14159']
```

## Nested List Comprehensions

_I think the case the too complicated._

### Example

``` python
>>> matrix = [
...     [1, 2, 3, 4],
...     [5, 6, 7, 8],
...     [9, 10, 11, 12],
... ]
```

transpose the row and column

``` python
>>> [[row[i] for row in matrix] for i in range(4)]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

equals:

``` python
>>> list(zip(*matrix))
[(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)]
```

## del statement

* Remove a item from list given index instead of its value
* Remove slices from a list
* Clear the entire list


``` python
>>> a = [-1, 1, 66.25, 333, 333, 1234.5]
>>> del a[0]
>>> a
[1, 66.25, 333, 333, 1234.5]
>>> del a[2:4]
[1, 66.25, 1234.5]
>>> del a[:]
>>> a
[]
```
* **delte entire variables:**

``` python
>>> del a
```

Referencing the name a hereafter is an error (at least until another value is assigned to it). We’ll find other uses for del later.

## Tuples

* Immutable
* Can contain mutable objects
* Init with or without surrounding parenthese

``` python
>>> empty = ()
>>> singleton = 'hello',    # <-- note trailing comma
>>> len(empty)
0
>>> len(singleton)
1
>>> singleton
('hello',)
```

_**sequence pack and unpack:**_

```python
>>> t = 12345, 54321 , 'hello'
>>> x, y, z = 6
>>> x
12345
```

## Sets

* A set is an unordered collection with no duplicate elements. 
* To create an empty set you have to use set(), not {}.

``` python
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
>>> 'orange' in basket                 # fast membership testing
True
>>> 'crabgrass' in basket
False

>>> # Demonstrate set operations on unique letters from two words
...
>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}
>>> a - b                              # letters in a but not in b
{'r', 'd', 'b'}
>>> a | b                              # letters in a or b or both
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # letters in both a and b
{'a', 'c'}
>>> a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}
```

``` python
>>> a = {x for x in 'abracadabra' if x not in 'abc'}
>>> a
{'r', 'd'}
```

## Dictionaries

* A dictionary as an unordered set of key: value pairs
* Keys are unique 
* A pair of braces creates an empty dictionary: `{}`.
* Delete a key:value pair： `del`
* An error to extract a value using a non-existent key.
* Placing a comma-separated list of key:value pairs within the braces adds initial key:value pairs to the dictionary

```python
>>> tel = {'jack': 4098, 'sape': 4139}
>>> tel['guido'] = 4127
>>> tel
{'sape': 4139, 'guido': 4127, 'jack': 4098}
>>> tel['jack']
4098
>>> del tel['sape']
>>> tel['irv'] = 4127
>>> tel
{'guido': 4127, 'irv': 4127, 'jack': 4098}
>>> list(tel.keys())
['irv', 'guido', 'jack']
>>> sorted(tel.keys())
['guido', 'irv', 'jack']
>>> 'guido' in tel
True
>>> 'jack' not in tel
False
```

_**Constructor:**_

```python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'jack': 4098, 'guido': 4127}

>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}

>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'jack': 4098, 'guido': 4127}
```

## Looping

### loop through dictionaries

```python
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...
gallahad the pure
robin the brave
```

### When looping through a sequence

The position index and corresponding value can be retrieved at the same time using the `enumerate()` function.

```python
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)
...
0 tic
1 tac
2 toe
```

### loop two more sequences

the entries can be paired with the `zip()` function.

```python
>>> questions = ['name', 'quest', 'favorite color']
>>> answers = ['lancelot', 'the holy grail', 'blue']
>>> for q, a in zip(questions, answers):
...     print('What is your {0}?  It is {1}.'.format(q, a))
...
What is your name?  It is lancelot.
What is your quest?  It is the holy grail.
What is your favorite color?  It is blue.
```

## MISC

### Build-in function

* `zip()`
* `resersed()`
* `sorted()`

### Conditions

* in / not in
* is / is not
* and / or
* _short-circuit_

### Comparing Sequences

* Compare by sequence
* Less means smaller
* Order for stirngs uses the Unicode code
* Mixed numeric types are compared according to their numeric value

``` python
(1, 2, 3)              < (1, 2, 4)
[1, 2, 3]              < [1, 2, 4]
'ABC' < 'C' < 'Pascal' < 'Python'
(1, 2, 3, 4)           < (1, 2, 4)
(1, 2)                 < (1, 2, -1)
(1, 2, 3)             == (1.0, 2.0, 3.0)
(1, 2, ('aa', 'ab'))   < (1, 2, ('abc', 'a'), 4)
```