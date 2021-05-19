# python tool box

## 1. user-defined function

Doctrings

```python
def square(value):
	"""Return the square of r value"""
 	new_value = value ** 2
# print(new_value)
 	return new_value
```

return tuples

tuples:

- like a list - can contain multiple values
- immutable - can't modify values!
- constructed using parenthesis()

unpack

`nums` is a tuples with 3 numbers.
`num1, num2, num3 = nums`

## 2. Default arguments, variable-length arguments and scope

1. Scope

- Global scope - defined in the main body.
- Local scope - defined inside a function.
- built-in scope - names in the pre-defined built in module

scope search order:

1. local scope
2. Enclosing functions
3. global scope
4. built-in scope

```python
def suqare(value):
	global new_val 		##modify global variable in function
	new_val = new_val ** 2
	return new_val
```

2. Nested function

```python
def echo(n):
    """Return the inner_echo function."""
    # Define inner_echo
    def inner_echo(word1):
        """Concatenate n copies of word1."""
        echo_word = word1 * n
        return echo_word
    # Return inner_echo
    return inner_echo

# Call echo: twice
twice = echo(2)

# Call echo: thrice
thrice = echo(3)

# Call twice() and thrice() then print
print(twice('hello'), thrice('hello'))
```
the outer function calls the inner function multiple times.

- variable-length arguments `(*args)`
- variable-length keywords arguments `(**kwargs)` dictionary.
```python
# Define report_status
def report_status(**kwargs):
    """Print out the status of a movie character."""

    print("\nBEGIN: REPORT\n")

    # Iterate over the key-value pairs of kwargs
    for key, value in kwargs.items():
        # Print out the keys and values, separated by a colon ':'
        print(key + ": " + value)

    print("\nEND REPORT")
# Second call to report_status()
report_status(name="luke", affiliation="jedi", status="missing")
```
