## Filtering data

Sometimes we have data that contains values we don't want to use.
In NumPy, we can apply basic relation operations element-wise on arrays.

```python
arr = np.array([[0, 2, 3],
                [1, 3, -6],
                [-3, -2, 1]])
print(repr(arr == 3)) # -> array([[False, False, True], [False, True, False], [False, False, False]])
print(repr(~(arr != 1))) # -> array([[False, False, False], [True, False, False], [False, False, True]])
```

Something to note is that `np.nan` can't be used with any relation operation. Instead, we use [np.isnan](https://docs.scipy.org/doc/numpy/reference/generated/numpy.isnan.html) to filter for the location of `np.nan`.

```python
arr = np.array([[0, 2, np.nan],
                [1, np.nan, -6],
                [np.nan, -2, 1]])
print(repr(~np.isnan(arr))) # -> array([[True, True, False], [True, False, True], [False, True, True]])
```

Each boolean array in our examples represents the location of elements 
we want to filter for. The way we perform the filtering itself is through the [np.where](https://docs.scipy.org/doc/numpy/reference/generated/numpy.where.html) function.

## Filtering in NumPy

The `np.where` function takes in a required first argument, which is a boolean array where `True` represents the location of the elements we want to filter for. When 
the function is applied with only the first argument, it returns a tuple of 1-D arrays.

The tuple will have size equal to the number of dimensions in the data, and each array represents the `True` indices for the corresponding dimension. Note that arrays in the tuple will all have the same length, equal to the number of `True` elements in the input argument.

```python
arr = np.array([0, 3, 5, 3, 1])
print(repr(np.where(arr == 3))) # -> (array([1, 3]),)

arr = np.array([[0, 2, 3],
                [1, 0, 0],
                [-3, 0, 0]])
x_ind, y_ind = np.where(arr != 0)
print(repr(x_ind)) # x-axis indices of non-zero elements
print(repr(y_ind)) # y-axis indices of non-zero elements
print(repr(arr[x_ind, y_ind])) # -> array([2, 3, 1, -3])
```

The interesting thing about `np.where` is that it must be applied with exactly 1 or 3 arguments. When we use 3 arguments, the first argument is still the boolean array. However, the next two arguments represent the `True` replacement values and the `False` replacement values, respectively. The output of the function now becomes an array with the same shape as the first argument.

```python
np_filter = np.array([[True, False], [False, True]])
positives = np.array([[1, 2], [3, 4]])
negatives = np.array([[-2, -5], [-1, -8]])
print(repr(np.where(np_filter, positives, negatives))) # -> array([[1, -5], [-1, 4]])
```

Note that our second and third arguments should necessarily have the same shape 
as the first argument. However, if we wanted to use a constant replacement value, e.g. `-1`, we could incorporate [broadcasting](https://docs.scipy.org/doc/numpy/user/basics.broadcasting.html). Rather than using an entire array of the same value, we can just use the value itself as an argument.

```python
np_filter = np.array([[True, False], [False, True]])
positives = np.array([[1, 2], [3, 4]])
print(repr(np.where(np_filter, positives, -1))) # -> array([[1, -1], [-1, 4]])
```

## Axis-wise filtering

If we wanted to filter based on rows or columns of data, we could use the [np.any](https://docs.scipy.org/doc/numpy/reference/generated/numpy.any.html) and [np.all](https://docs.scipy.org/doc/numpy/reference/generated/numpy.all.html) functions. Both functions take in the same arguments, and return a single boolean or a boolean array. The required argument for both functions is a boolean array.

```python
arr = np.array([[-2, -1, -3],
                [4, 5, -6],
                [3, 9, 1]])
print(np.any(arr > 0)) # -> True
print(np.all(arr > 0)) # -> False
```

The `np.any` function is equivalent to performing a logical OR (`||`), while the `np.all` function is equivalent to a logical AND (`&&`) on the first argument. When only a single argument is passed in, the function is applied across the entire input array, so the returned value is a single boolean.

However, if we use a multi-dimensional input and specify the `axis` keyword argument, the returned value will be an array. The `axis` argument has the same meaning as it did for `np.argmin` and `np.argmax` from the previous chapter.

```python
arr = np.array([[-2, -1, -3],
                [4, 5, -6],
                [3, 9, 1]])
print(repr(np.any(arr > 0, axis=0))) # -> array([True, True, True])
print(repr(np.any(arr > 0, axis=1))) # -> array([False, True, True])
```

We can use `np.any` and `np.all` in tandem with `np.where` to filter for entire rows or columns of data.

```python
arr = np.array([[-2, -1, -3],
                [4, 5, -6],
                [3, 9, 1]])
has_positive = np.any(arr > 0, axis=1) # -> [False, True, True]
print(repr(arr[np.where(has_positive)])) # -> array([[4, 5, -6], [3, 9, 1]])
```
