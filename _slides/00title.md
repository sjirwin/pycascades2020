---
title: Main title
---

## Reflected Binary Operators
#### Why `3*'spam '` is `'spam spam spam '`

<span style="font-size:smaller">PyCascades &mdash; 2020</span>
<center>
Scott Irwin<br/>
<img src="images/bloomberg-logo-black.svg"
     style="border: none; box-shadow: none; height: 45px"
     alt="Bloomberg"><br/>
<p>&nbsp;<p>
https://sjirwin.github.io/pycascades2020/
</center>

--

## Reflected Operators
- All of the numerical operators have a reflected version
  - <span style="color:indianred">`__rmul__`</span>, <span style="color:indianred">`__radd__`</span>, etc.
- _Right operand_'s reflected operation is called if the left operand's method returns <span style="color:indianred">`NotImplemented`</span> **and** the operands are different types

--

## Reflected Operator Example
- <span style="color:indianred">`a * b`</span>
  - First call <span style="color:indianred">`a.__mul__(b)`</span>
  - If that returns <span style="color:indianred">`NotImplemented`</span> **and** <span style="color:indianred">`a`</span> and <span style="color:indianred">`b`</span> are different types, then call <span style="color:indianred">`b.__rmul__(a)`</span>

--

## `3 * 'spam ' works`
- It is easy to show that multiplying a `int` and a `str` works
``` python
>>> 3 * 'spam '
'spam spam spam '
```

--

## But `(3).__mul__('spam ') does not`
- The <span style="color:indianred">`*`</span> operator is implemented via <span style="color:indianred">`__mul__()`</span>
- So <span style="color:indianred">`3 * 'spam '`</span> is the same thing as <span style="color:indianred">`(3).__mul__('spam ')`</span>

``` python
>>> (3).__mul__('spam ')
NotImplemented
```

- This happens because the <span style="color:indianred">`__mul__()`</span> defined in the `int` class does not know how to multiply itself with a `str`

--

## `__rmul__()` to the rescue

- String "multiplication" works because <span style="color:indianred">`3`</span> and <span style="color:indianred">`'spam '`</span> are different types
- When <span style="color:indianred">`__mul__()`</span> returns <span style="color:indianred">`NotImplemented`</span>, Python then tries the reflected operator <span style="color:indianred">`__rmul__()`</span> defined in the `str` class
  - <span style="color:indianred">`3 * 'spam '`</span> becomes <span style="color:indianred">`'spam '.__rmul__(3)`</span>

``` python
>>> 'spam '.__rmul__(3)
'spam spam spam '
```
