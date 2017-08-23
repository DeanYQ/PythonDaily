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

## Search Path

* The directory containing the input script (or the current directory)
* PYTHONPATH (a list of directory names, with the same syntax as the shell variable PATH).
* The installation-dependent default.

_Note: modify the sys.path to make the scripts in the targeted directory will be loaded ahead of the standard library path._

## Compile Module

* Python check modification and verify whether it need to be recomiple
* Command line doesn't check cache.
* Non-source distribution doesn't check cache.
* .pyc dosn't run faster than .py. Just speed up during loading module.

## Standard Modules

* core of language
* built into the interpreter to access operating system primitives.

The variables `sys.ps1` and `sys.ps2` define the string sused as primary and secondary prompt. They are only defined if the interpreter is in  interactive mode.

```python
>>> import sys
>>> sys.ps1
'>>> '
>>> sys.ps2
'... '
>>> sys.ps1 = 'C> '
C> print('Yuck!')
Yuck!
C>
```
