# How to handle FILES(including STDIN, STDOUT) and format IO


## Formatting string
### Current Standard for string formatting(using `f` string or `str.format()` method)
`f` string is same as `str.format()` method. `str.format` came earlier. All things applied to `str.format` is also applied to `f` strings.

### `f` string style
```python
occupation = "mechanic"
age = 23
print(f"Hi! I am a {occupation}. I'm {age} years old.")
```

### `str.format` style
`str.format` is a bit flexible. It has several ways to format strings. Let's see one by one:

1. style-01: default order
```python
occupation = "mechanic"
age = 23
print("Hi! I am a {}. I'm {} years old.".format(occupation, age))
```

2. style-02: by index
```python
occupation = "mechanic"
age = 23
# note that occupation comes later
print("Hi! I am a {1}. I'm {0} years old.".format(age, occupation))
```

3. style-03: named argument
```python
occupation = "mechanic"
age = 23
# note that occupation comes later
print("Hi! I am a {}. I'm {my_age} years old.".format(occupation, my_age=age))
```

4. style-04: dictionary unpacking
```python
person = {
    'occupation': 'mechanic',
    'age': 23
}
print("Hi! I am a {occupation}. I'm {age} years old.".format(**person))
```
Note: you can mix unpacking with positional and named arguments.

5. style-05: list/tuple unpacking
```python
person = ("mechanic", 23)
print("Hi! I am a {}. I'm {} years old.".format(*person))
```

### General formatting rule guide for `f` string or `str.format`
```bash
format_spec     ::=  [[fill]align][sign][#][0][width][grouping_option][.precision][type]
fill            ::=  <any character>
align           ::=  "<" | ">" | "=" | "^"
sign            ::=  "+" | "-" | " "
width           ::=  digit+
grouping_option ::=  "_" | ","
precision       ::=  digit+
type            ::=  "b" | "c" | "d" | "e" | "E" | "f" | "F" | "g" | "G" | "n" | "o" | "s" | "x" | "X" | "%"
```

Here, `format_spec` denotes the way one can format a input given in `f-string` or `str.format`. A basic example:
```python
print("{:_>#12b}".format(24))
# it outputs
# _____0b11000
```
Explanation of the example:
1. `:` is the seperator between input value and decorator/format-spec
2. `_` it represents fill
3. `>` it means `right align`
4. `#` is a special symbol. you know, 24(in decimal) = 11000(in binary). But you can see in the output `11000` is prefixed with `0b` i.e. `0b11000`. `#` added the `0b`. If you don't want to add the `radix/base prefix`, then just omit `#`
5. `b` represents type. Here, `b` means binary type. Hence, `24` is written as `11000`.


### More on formatting later...
