## Statistical metrics

NumPy provides basic statistical functions such as [np.mean](https://docs.scipy.org/doc/numpy/reference/generated/numpy.mean.html), [np.var](https://docs.scipy.org/doc/numpy/reference/generated/numpy.var.html), and [np.median](https://docs.scipy.org/doc/numpy/reference/generated/numpy.median.html), to calculate the mean, variance, and median of the data, respectively.

```python
arr = np.array([[0, 72, 3],
                [1, 3, -60],
                [-3, -2, 4]])
print(np.mean(arr)) # -> 2.0
print(np.var(arr)) # -> 977.3(3)
print(np.median(arr)) # -> 1.0
print(repr(np.median(arr, axis=1))) # -> array([3., 1., -2.])
```

Each of these functions takes in the data array as a required argument and `axis` as a keyword argument. For a more comprehensive list of statistical functions (e.g. calculating percentiles, creating histograms, etc.), check out the NumPy [statistics page](https://docs.scipy.org/doc/numpy/reference/routines.statistics.html).


