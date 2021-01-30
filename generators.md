# Generators

## Contents

- [Generators](#generators)
  - [Contents](#contents)
  - [Comparison](#comparison)

A generator can be created by using *generator functions* or *generator expresssions*. Both of them return a **lazy iterator**. Iterators in general, unlike lists for example, don't store their contents in memory.

```python
def inifinite_sequence():
    num = 0
    while True:
        yield num
        num += 1
```

> Normally you don't want to write your own iterator. `itertools` provides iterators for efficient looping.

As you see, generators are very similar to functions. However, generators use `yield` statement rather than what functions use, the `return` statement. In generators, statements are executed up until yield `statement`. However, unlike functions, the state of the generator function is kept, and when `next()` is called on the same generator object, the execution continues where it left off.

As for generator comprehensions, they work syntactically in the same way as list comprehensions do. For example:

```python
nums_squred_lc = [x**2 for x in range(10)]
nums_squred_gc = (x**2 for x in range(10))
```

## Comparison

When memory is more critical than speed, generators are way to go. Let's compare memory:

```python
import sys

nums_squred_lc = [x**2 for x in range(10)]
nums_squred_gc = (x**2 for x in range(10))

print(sys.getsizeof(nums_squred_lc))
print(sys.getsizeof(nums_squred_gc))
```

Let's compare speed:

```python
import cProfile

cProfile.run("sum([x**2 for x in range(10000)])")
cProfile.run("sum((x**2 for x in range(10000)))")
```