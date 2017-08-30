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

## dir()

`dir()` is used to find out which names a module defines. It returns a sorted list of strings.

```python
>>> import fibo, sys
>>> dir(fibo)
['__name__', 'fib', 'fib2']
>>> dir(sys)  
['__displayhook__', '__doc__', '__excepthook__', '__loader__', '__name__',
 '__package__', '__stderr__', '__stdin__', '__stdout__',
 '_clear_type_cache', '_current_frames', '_debugmallocstats', '_getframe',
 '_home', '_mercurial', '_xoptions', 'abiflags', 'api_version', 'argv',
 'base_exec_prefix', 'base_prefix', 'builtin_module_names', 'byteorder',
 'call_tracing', 'callstats', 'copyright', 'displayhook',
 'dont_write_bytecode', 'exc_info', 'excepthook', 'exec_prefix',
 'executable', 'exit', 'flags', 'float_info', 'float_repr_style',
 'getcheckinterval', 'getdefaultencoding', 'getdlopenflags',
 'getfilesystemencoding', 'getobjects', 'getprofile', 'getrecursionlimit',
 'getrefcount', 'getsizeof', 'getswitchinterval', 'gettotalrefcount',
 'gettrace', 'hash_info', 'hexversion', 'implementation', 'int_info',
 'intern', 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path',
 'path_hooks', 'path_importer_cache', 'platform', 'prefix', 'ps1',
 'setcheckinterval', 'setdlopenflags', 'setprofile', 'setrecursionlimit',
 'setswitchinterval', 'settrace', 'stderr', 'stdin', 'stdout',
 'thread_info', 'version', 'version_info', 'warnoptions']
 ```

Without arguments, `dir()` lists the names you have defined currently.

```python
>>> a = [1, 2, 3, 4, 5]
>>> import fibo
>>> fib = fibo.fib
>>> dir()
['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']
```

dir() doesn't list the names of built-in functions and variables. If you want to a list of those, they are defined in the standard module `builtins`:

```python
>>> import builtins
>>> dir(builtins)  
['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException',
 'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning',
 'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError',
 'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning',
 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False',
 'FileExistsError', 'FileNotFoundError', 'FloatingPointError',
 'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError',
 'ImportWarning', 'IndentationError', 'IndexError', 'InterruptedError',
 'IsADirectoryError', 'KeyError', 'KeyboardInterrupt', 'LookupError',
 'MemoryError', 'NameError', 'None', 'NotADirectoryError', 'NotImplemented',
 'NotImplementedError', 'OSError', 'OverflowError',
 'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError',
 'ReferenceError', 'ResourceWarning', 'RuntimeError', 'RuntimeWarning',
 'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError',
 'SystemExit', 'TabError', 'TimeoutError', 'True', 'TypeError',
 'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError',
 'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning',
 'ValueError', 'Warning', 'ZeroDivisionError', '_', '__build_class__',
 '__debug__', '__doc__', '__import__', '__name__', '__package__', 'abs',
 'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable',
 'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits',
 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit',
 'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr',
 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass',
 'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview',
 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property',
 'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice',
 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars',
 'zip']
```

## Packages

* A way of structuring Python's module namespace.
* When importing the package, Python searchs through the directories on `sys.path` looking for the package subdirectory.

### `__init__.py`
The `__init__.py` files are required to make Python treat the directories as a containing package.  
`_init_.py` can just be an empty file, but it can also execute initialization code for the package or set the `__all__` variable.

#### case 1

``` python
import sound.effects.echo
```

Load submodule, it must be referenced with its full name.

``` python
sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
```

#### case 2

``` python
from sound.effects import echo
echo.echofilter(input, output, delay=0.7, atten=4)
```

#### case 3

```python
from sound.effects.echo import echofilter
```

_**Note:**_:  
1. `from package import item`, the item can be either a submodule (or subpakcage) or the package, or some other name defined in the package, like function, class or variable. The `import` statement first tests whether the item is defined in the package; if not, it assumes it is a module and attempts to load it. If it fails to find it, an ImportError exception is raised.

2. `import item.subitem.subsubitem`, each item except for the last must be a package; the last item can be a module or a package but can't be a class or function or variable defined in the previous item.

## Others

* `__all__`:  
if `__all__` is defined in the `__init__.py`, the `from package import *` will import the names listed in the `__all__`, otherwise the package will import whatever names defined in the package.

* Intra-package:  
Relative import. Note that relative imports are based on the name of the current module. Since the name of the main module is always `__main__`, modules intended for use as the main module of a Python application must always use absolute imports.

* `__path__`:  
Packages support one more special attribute, __path__. This is initialized to be a list containing the name of the directory holding the package’s __init__.py before the code in that file is executed. This variable can be modified; doing so affects future searches for modules and subpackages contained in the package.

