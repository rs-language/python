# Basics of python


## Conditionals
### if construct
#### if/else construct
```python
n = 2
if n > 1:
    print(f"{n} is greater than 1")
else:
    print(f"{n} is equal to or less han 1")
```
#### if/else ladder construct
```python
n = 23
if n < 0:
    print(f"{n} is negative")
elif n == 0:
    print(f"{n} is 0")
else:
    print(f"{n} is positive")
```

## Loop constructs

### `for` loop
#### iterate over a range of elements
```python
end = 10
for i in range(end):
    print(i)
# prints 0 to 9

start = -3
for i in range(start, end):
    print(i)
# prints -3 to 9

step = 3
for i in range(start, end, step):
    print(i)
# prints -3, -1, 1, 3, 5, 7, 9
```

#### iterate over array using for loop
```python
arr = [1, 2, 3, 4, 5]
for v in arr:
    print(v)
# prints the array elements
```

#### iterate over array using with index
1. with the help of `enumerate`:
```python
arr = [5, 4, 3, 2, 1]
for i, v in enumerate(arr):
    print(f"value at index {i} is {v}")
# prints index number and corresponding value
```
2. with the help of `range`:
```python
arr = [5, 4, 3, 2, 1]
for i in range(len(arr)):
    print(f"value at index {i} is {arr[i]}")
# prints index number and corresponding value
```

#### iterate over dictionary items
```python
d = {5: "elo", 1: "melo", 3: "helo", 2: "khelo", 4: "gelo"}
for k, v in d.items():
    print(f"{k}: {v}")
# prints key/value pairs
```

#### iterate over set items
```python
st = {1, 2, 1, 2, 5, 4, 7, 7}
for x in st:
    print(x)
# prints 1, 2, 4, 5, 7
```

### while loop
```python
i, n = 1, 10
while i < n:
    print(i)
    i += 1
# prints 1, 2, ..., 9
```

### Loop break or skipping elements
#### Break i.e. Just stop the loop right now
```python
a = [1, 2, 3, 4, 5]
for v in a:
    print(v)
    if v == 3:
        break
# prints 1, 2, 3
```
#### Continue i.e. skip the current element
```python
a = [1, 2, 3, 4, 5]
for v in a:
    if v % 2 == 0:
        continue
    print(v)
# prints only odd numbers i.e. 1, 3, 5 and skips the even ones
```

## Functions
### Function parameters
In python we can pass arguments to function either
- by position or
- by keywords
  
A function definition may look like:
```python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```
where `/` and `*` are optional. If used, these symbols indicate the kind of parameters by how the arguments may be passed to the function: `positional-only`, `positional-or-keyword`, and `keyword-only`. `Keyword parameters` are also referred to as `named parameters`.

#### Default arg behavior/Standard arg behavior
If `/` and `*` are not present in the function definition, arguments may be passed to a function by position or by keyword.
```python
def default_arg_demo(a1, a2):
    print(f"a1: {a1}, a2: {a2}")

default_arg_demo(1, 2) # prints 1 and 2
default_arg_demo(a2=2, a1=1) # prints 1 and 2
default_arg_demo(1, a2=2) # prints 1 and 2
```

#### Position only arg
If you want to use only position-only arg, then just terminate the args list with `/`. Examples given below:
```python
def pos_only_arg(arg, /):
    print(arg)

pos_only_arg(1) # prints 1
pos_only_arg(arg=1) # throws TypeError
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: pos_only_arg() got an unexpected keyword argument 'arg'
```

#### Keyword only arg
```python
def kwd_only_arg(*, arg):
    print(arg)
kwd_only_arg(3) # throws TypeError
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: kwd_only_arg() takes 0 positional arguments but 1 was given
kwd_only_arg(arg=3) # prints 3
```

#### Combined i.e. pos-only, standard, and kw-only all three
```python
def combined_example(pos_only, /, standard, *, kwd_only):
    print(pos_only, standard, kwd_only)

combined_example(1, 2, 3) # throws TypeError
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: combined_example() takes 2 positional arguments but 3 were given

combined_example(1, 2, kwd_only=3) # prints 1 2 3

combined_example(1, standard=2, kwd_only=3) # prints 1 2 3

combined_example(pos_only=1, standard=2, kwd_only=3)
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: combined_example() got an unexpected keyword argument 'pos_only'
```

### Variable number of arguments passing in function
#### Passing variable number of non-named args
```python
def sum(*args):
    # here args type is `tuple`
    s = 0
    for v in args:
        s += v
    return s

sum(1, 2, 3, 4, 5) # returns 15
# you may also do as follows, i.e. use tuple insted of list
arr = [1, 2, 3, 4, 5]
# or arr = (1, 2, 3, 4, 5)
sum(*arr) # returns 15
```
#### Passing variable number of named arguments
```python
def student(**kwargs):
    for k, v in kwargs.items():
        print(f"{k}: {v}")

student(name="reyad", age=23) # it prints
# name: legend
# age: 23

# you may also do as follows
student(**{
    "name": "legend",
    "age": 23
}) # it also prints
# name: legend
# age: 23
```

#### Passing variable number of arguments combined i.e. normal, \*args, and \*\*kwargs
```python
def combined(pos1, pos2, *args, **kwargs):
    print(f"normal: {pos1} and {pos2}")
    print(f"variable args(non-named): {args}")
    print(f"variable args(named): {kwargs.items()}")

combined("_pos1_", "_pos2_", 1, 2, 3, name="reyad", age=23)
# output
# normal: _pos1_ and _pos2_
# variable args(non-named): (1, 2, 3)
# variable args(named): dict_items([('name', 'reyad'), ('age', 23)])
```