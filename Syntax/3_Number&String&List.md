# Number

1. basic

``` Python
+ - * / %
```

2. advanced

Power : **
``` Python
>>> 5 ** 2
```

In interactive mode, the last printed expression is assigned to the variable _.

``` Python
>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round(_, 2)
113.06
```

# String
1. Enclosed in single quotes ('...') or double quotes ("...") with the same result.

``` Python
>>> 'spam eggs'  # single quotes
'spam eggs'
>>> 'doesn\'t'  # use \' to escape the single quote...
```

2. Raw string to avoid '\' (escape specal character)

``` Python
>>> print('C:\some\name')  # here \n means newline!
C:\some
ame
>>> print(r'C:\some\name')  # note the r before the quote
C:\some\name
```

3. Multiple lines. \n

One way is using triple-quotes: """...""" or '''...'''. End of lines are automatically included in the string, but it’s possible to prevent this by adding a \ at the end of the line

``` Python
print("""\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
""")


output:
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
```