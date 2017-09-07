# Errors And Exceptions

## Distinguish

* Errors: Parse error, syntax error.
* Exceptions: Run time during execution.

## Handle

`try` statement.

```python
>>> while True:
...     try:
...         x = int(input("Please enter a number: "))
...         break
...     except ValueError:
...         print("Oops!  That was no valid number.  Try again...")
...
```

An `except` clause may name multiple exceptions as parethesized tuple.

```python
... except (RuntimeError, TypeError, NameError):
...     pass
```

The first matching `except` clause will be triggered when an exception is raised.

The last `except` clause may omit exception name(s) to serve as wildcard.

```python
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
```

## Clause Keywords

### `else`

Follow all `except` clauses. It's exceuted if the `try` clause doesn't raise an exception.

```python
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

### `raise`

`raise` allow to force a specified exception occur.

```python
>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
```

### `finally`

A `finally` clause is always executed before leaving the `try` statement, whether an exception has occurred or not. It's also executed "on the way out" when left via `break`, `continue`, `return`.

```python
>>> def divide(x, y):
...     try:
...         result = x / y
...     except ZeroDivisionError:
...         print("division by zero!")
...     else:
...         print("result is", result)
...     finally:
...         print("executing finally clause")
...
>>> divide(2, 1)
result is 2.0
executing finally clause
>>> divide(2, 0)
division by zero!
executing finally clause
>>> divide("2", "1")
executing finally clause
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in divide
TypeError: unsupported operand type(s) for /: 'str' and 'str'
```

### `with`

`with` statement allows objects like files to be used in a way that ensures they are always cleaned up promptly and correctly

### `instance.args`

The `except` clause may specify a variable after the exception. The variable is bound to an exception instance with arguments stored in `instance.args`. The exception instance defines `__str()__` so the arguments can be printed directly without having to reference `.args`.

```python
>>> try:
...     raise Exception('spam', 'eggs')
... except Exception as inst:
...     print(type(inst))    # the exception instance
...     print(inst.args)     # arguments stored in .args
...     print(inst)          # __str__ allows args to be printed directly,
...                          # but may be overridden in exception subclasses
...     x, y = inst.args     # unpack args
...     print('x =', x)
...     print('y =', y)
...
<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
x = spam
y = eggs
```


## User-defined Exceptions

* Keep user-defined exception simple.
* Define with names end in "Error"

```python
class Error(Exception):
    """Base class for exceptions in this module."""
    pass

class InputError(Error):
    """Exception raised for errors in the input.

    Attributes:
        expression -- input expression in which the error occurred
        message -- explanation of the error
    """

    def __init__(self, expression, message):
        self.expression = expression
        self.message = message
```
