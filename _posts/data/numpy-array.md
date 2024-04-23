---
layout: post
title: "Map like function with NumPy and Pandas"
tags: ["python", "numpy"]
---

The best way is to create a numpy `ufunc` 

You can create your own custom ufuncs in NumPy using the numpy.frompyfunc() function or by using the numpy.vectorize() decorator. 

Custom ufuncs can be useful when you have a specific mathematical operation that you want to apply element-wise to arrays. They provide a way to extend NumPy's functionality with your own custom functions.

1. **numpy.frompyfunc:**
   - **Purpose:** `numpy.frompyfunc` creates a universal function (ufunc) from an ordinary Python function.
   - **Parameters:**
     - `func`: The Python function that you want to convert into a ufunc.
     - `nin`: Number of input arguments expected by the function.
     - `nout`: Number of output arguments returned by the function.
   - **Returns:** A ufunc object.

2. **numpy.vectorize:**
   - **Purpose:** `numpy.vectorize` is a class that transforms a Python function taking scalar inputs into a vectorized function.
   - **Parameters:**
     - `pyfunc`: The Python function you want to vectorize.
     - `otypes`: Output data types of the vectorized function. Default is `None`.
     - `doc`: Optional docstring for the vectorized function.
     - `excluded`: Indices or slices of arguments to exclude from vectorization. Default is `None`.
     - `cache`: If True, cache the first function call. Default is False.
     - `signature`: Signature of the vectorized function. Default is `None`.

Here are examples of creating custom ufuncs using both methods

```py
import numpy as np

# create the function you want to execute
f = lambda x, y: x * y

# alternative 1
f_arr = np.frompyfunc(f, 2, 1)

# alternative 1
vf = np.vectorize(f)

# create the numpy array
arr = np.linspace(0, 1, 10000)

# performance
%timeit f_arr(arr, arr) # 307ms
%timeit vf(arr, arr) # 450ms
```

Both `frompyfunc` and `vectorize` serve similar purposes, but they have some differences in usage and behavior. `frompyfunc` is generally faster but less flexible than `vectorize`. Additionally, `vectorize` allows more control over the output data types and other aspects of the vectorized function.

https://stackoverflow.com/questions/35215161/most-efficient-way-to-map-function-over-numpy-array

`numpy.frompyfunc` and `numpy.vectorize` are two functions in the NumPy library that allow you to create universal functions (ufuncs) from Python functions. These functions can then be applied element-wise to arrays.

Here's a brief explanation of each along with the parameters they need:

