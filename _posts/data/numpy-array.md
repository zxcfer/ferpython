---
layout: post
title: "Map like function with NumPy"
tags: ["python", "numpy"]
---

The best way is to create a numpy `ufunc` 

```py
import numpy as np

f = lambda x, y: x * y
f_arr = np.frompyfunc(f, 2, 1)
vf = np.vectorize(f)
arr = np.linspace(0, 1, 10000)

%timeit f_arr(arr, arr) # 307ms
%timeit vf(arr, arr) # 450ms
```

https://stackoverflow.com/questions/35215161/most-efficient-way-to-map-function-over-numpy-array