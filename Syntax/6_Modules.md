# Modules

## Global variables

* `__name__`

```python
>>> fibo.fib(1000)
1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
>>> fibo.fib2(100)
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
>>> fibo.__name__
'fibo'
```

* `__main__`

Indicate whether the module is executed as the “main” file:

```python
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```

## import

* `import` module

```python
>>> import fibo
>>> fib = fibo.fib
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
'fibo'
```

* `from` module `import` function

There is a variant of the import statement that imports names from a module directly into the importing module’s symbol table.

```python
>>> from fibo import fib, fib2
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

* `from` module `import` *

```python
>>> from fibo import *
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

**Note**: _For efficiency reasons, each module is only imported once per interpreter session. Therefore, if you change your modules, you must restart the interpreter – or, if it’s just one module you want to test interactively, use importlib.reload(), e.g. import importlib; importlib.reload(modulename)._

```python
>>> import importlib
>>> importlib.reload(modulename).
```