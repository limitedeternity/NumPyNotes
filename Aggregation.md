## Summation

To sum the values within a single array, we use the [np.sum](https://docs.scipy.org/doc/numpy/reference/generated/numpy.sum.html) function.

```python
arr = np.array([[0, 72, 3],
                [1, 3, -60],
                [-3, -2, 4]])
print(np.sum(arr)) # -> 18
print(repr(np.sum(arr, axis=0))) # -> array([-2, 73, -53])
print(repr(np.sum(arr, axis=1))) # -> array([75, -56, -1])
```

In addition to regular sums, NumPy can perform cumulative sums using [np.cumsum](https://docs.scipy.org/doc/numpy/reference/generated/numpy.cumsum.html). Like `np.sum`, `np.cumsum` also takes in a NumPy array as a required argument and uses the `axis` argument. If the `axis` keyword argument is not specified, `np.cumsum` will return the cumulative sums for the flattened array.

```python
arr = np.array([[0, 72, 3],
                [1, 3, -60],
                [-3, -2, 4]])
print(repr(np.cumsum(arr))) # -> array([ 0, 72, 75, 76, 79, 19, 16, 14, 18])
print(repr(np.cumsum(arr, axis=0))) # -> array([[0, 72, 3], [1, 75, -57], [-2, 73, -53]])
print(repr(np.cumsum(arr, axis=1))) # -> array([[0, 72, 75], [1, 4, -56], [-3, -5, -1]])
```

## Concatenation

An important part of aggregation is combining multiple datasets. In NumPy, this equates to combining multiple arrays into one. The function we use to do this is [np.concatenate](https://docs.scipy.org/doc/numpy/reference/generated/numpy.concatenate.html).

Like the summation functions, `np.concatenate` uses the `axis` keyword argument. However, the default value for `axis` is `0`. Furthermore, the required argument for `np.concatenate` is a list of arrays, which the function combines into a single array.

```python
arr1 = np.array([[0, 72, 3],
                 [1, 3, -60],
                 [-3, -2, 4]])
arr2 = np.array([[-15, 6, 1],
                 [8, 9, -4],
                 [5, -21, 18]])
print(repr(np.concatenate([arr1, arr2])))
print(repr(np.concatenate([arr1, arr2], axis=1)))

"""
array([[  0,  72,   3],
       [  1,   3, -60],
       [ -3,  -2,   4],
       [-15,   6,   1],
       [  8,   9,  -4],
       [  5, -21,  18]])
array([[  0,  72,   3, -15,   6,   1],
       [  1,   3, -60,   8,   9,  -4],
       [ -3,  -2,   4,   5, -21,  18]])
"""
```
