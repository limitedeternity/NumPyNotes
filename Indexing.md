## Array accessing

Accessing NumPy arrays is identical to accessing Python lists. For multi-dimensional arrays, it is equivalent to accessing Python lists of lists.

## Slicing

NumPy arrays also support slicing. Similar to Python, we use the colon operator (i.e. `arr[:]`) for slicing. We can also use negative indexing to slice in the backwards direction.

For multi-dimensional arrays, we can use a comma to separate slices across each dimension.

```python
arr = np.array([[1, 2, 3],
                [4, 5, 6],
                [7, 8, 9]])
print(repr(arr[:, -1])) # -> array([3, 6, 9])
print(repr(arr[:, 1:])) # -> array([[2, 3], [5, 6], [8, 9]])
print(repr(arr[0:1, 1:])) # -> array([[2, 3]])
print(repr(arr[0, 1:])) # -> array([2, 3])
```

## Argmin and argmax

In addition to accessing and slicing arrays, it is useful to figure out the actual indexes of the minimum and maximum elements. To do this, we use the [np.argmin](https://docs.scipy.org/doc/numpy/reference/generated/numpy.argmin.html) and [np.argmax](https://docs.scipy.org/doc/numpy/reference/generated/numpy.argmax.html) functions.

The `np.argmin` and `np.argmax` functions take the same arguments – the required argument, which is an input array, and the `axis` keyword argument, which specifies an index of dimension to apply the operation to.

```python
arr = np.array([[-2, -1, -3],
                [4, 5, -6],
                [-3, 9, 1]])
print(np.argmax(arr[0])) # -> 1
print(np.argmin(arr)) # -> 5
print(repr(np.argmin(arr, axis=0))) # -> array([2, 0, 1])
print(repr(np.argmin(arr, axis=1))) # -> array([2, 2, 0])
```

In this case, `axis=0` makes function find an index of the minimum *row* element for each column. On the other hand, `axis=1` – an index of the minimum *column* element for each row.


