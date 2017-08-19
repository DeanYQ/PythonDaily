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