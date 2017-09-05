# Input And Output

## String Format

### string convert

* `str()`  
return a representations of values which are fairly human-readable

* `repr()`  
generate representations which can be read by interpreter.

__Note__: For objects which don't have particular representation for human comsupstion, `str()`  will return the same as `repr()`.

### Padding

* `.rjust()`: right justify a string in a field of given width by padding it with spaces on the left.

* `.ljust()`:
* `.center()`:
* `.zfill()`: pad a numberic string on the left with zeros. It understands about the plus and signs.

__Note__: If want string truncation, just use a slice operation, as `x.ljust(n)[:n]`.

### Format

`.format()`:

Example 1: 

```python
>>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
We are the knights who say "Ni!"
```

Example 2:  

```python
>>> print('{0} and {1}'.format('spam', 'eggs'))
spam and eggs
>>> print('{1} and {0}'.format('spam', 'eggs'))
eggs and spam
```

Example 3:

```python
>>> print('This {food} is {adjective}.'.format(
...       food='spam', adjective='absolutely horrible'))
This spam is absolutely horrible.
```

**_'!a' (apply `ascii()`), '!s' (apply `str()`) and '!r' (apply `repr()`) can be used to convert the value before it is formatted:_**

```python
>>> contents = 'eels'
>>> print('My hovercraft is full of {}.'.format(contents))
My hovercraft is full of eels.
>>> print('My hovercraft is full of {!r}.'.format(contents))
My hovercraft is full of 'eels'.
```

An optional `':'` and format specifier can follow the field name. This allows greater control over how the value is formatted

```python
>>> import math
>>> print('The value of PI is approximately {0:.3f}.'.format(math.pi))
The value of PI is approximately 3.142.
```

Passing an integer after the `':'` will cause that field to be a minimum number of characters wide.

```python
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
>>> for name, phone in table.items():
...     print('{0:10} ==> {1:10d}'.format(name, phone))
...
Jack       ==>       4098
Dcab       ==>       7678
Sjoerd     ==>       4127
```

User reference map name to format

```python
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>> print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
...       'Dcab: {0[Dcab]:d}'.format(table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678
```

This could also be done by passing the table as keyword arguments with the ‘**’ notation.

```python
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>> print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678
```

## File

* `open(filename, mode)`:  default mode is `'r'`

**_mode_**:  
`'r'` : file will only be read.  
`'w'` : file only for writing (an existing file with the same name will be erased).  
`'a'` : open the file for appending. Any data written to the file is automatically added to the end.  
`'r+'`: open the file for both reading and writing.


_**text_mode**_: If encoding is not specified, the default is platform dependent. `'b'` appended to the mode opens the file in _binary mode_.

_**Ending:**_: the default when reading is to convert platform-specific line endings (`\n` on Unix, `\r\n` on Windows)  to just `\n`.

* `with`:  
use `with` keyword when dealing with file objects.

```python
>>> with open('workfile') as f:
...     read_data = f.read()
>>> f.closed
True
```

* `f.close()`:  
 close the file and immediately free up any system resources used by it. If a file object is closed. either by a `with` statement or by calling `f.close()`, attempt to use the file object will automatically fail.

```python
>>> f.close()
>>> f.read()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: I/O operation on closed file
```

* `f.read(size)`:  
reads some quantity of data and returns it as a string (in text mode) or bytes object(in binary mode). _size_ is optional. When _size_ is omitted or negative, the entire contents of the file will be read and returned. If the end of file has been reached, `f.read()` will return an empoty string `('')`.

```python
>>> f.read()
'This is the entire file.\n'
>>> f.read()
''
```

* `f.readline()`:  
    * read a single line from the file;  
    * if `f.readline()` return an empty string, the end of the file has been reached;  
    * a blank line is represented by '\n', a string containing only a single newline.

```python
>>> f.readline()
'This is the first line of the file.\n'
>>> f.readline()
'Second line of the file\n'
>>> f.readline()
''
```

**Loop over the file object to read lines from a file.**

```python
>>> for line in f:
...     print(line, end='')
...
This is the first line of the file.
Second line of the file
```

**read all lines**: `list(f)` or `f.readlings()`  

* `f.write(string)`: writes the contents of `string` to the file, returning the number of characters written.

```python
>>> f.write('This is a test\n')
15
```

Other types of objects need to be converted --either a string (in atext mode) or a bytes object (in binary mode) --before writing them.

```python
>>> value = ('the answer', 42)
>>> s = str(value)  # convert the tuple to string
>>> f.write(s)
18
```

* `f.tell()`: return a integer giving  the file objects's current position in the file represented as number of bytes from the beginning of  the file when in binary mode and an opaque number when in text mode.

* `f.seek(offseet, from_what)`: to change the file object's position.

_from_what_ :  
0 beginning of the file.  
1 current file position  
2 end of the file as the reference point. 

If omitted and default is 0.

```python
>>> f = open('workfile', 'rb+')
>>> f.write(b'0123456789abcdef')
16
>>> f.seek(5)      # Go to the 6th byte in the file
5
>>> f.read(1)
b'5'
>>> f.seek(-3, 2)  # Go to the 3rd byte before the end
13
>>> f.read(1)
b'd'
```

## Json

_ref: pickle_

* `dumps()`
* `dump()`
* `load()`

```python
>>> import json
>>> json.dumps([1, 'simple', 'list'])
'[1, "simple", "list"]'
```

```python
json.dump(x, f)
```

```python
x = json.load(f)
```












