## Saving

After performing data manipulation with NumPy, it's a good idea to save the data in a file for future use. To do this, we use the [np.save](https://docs.scipy.org/doc/numpy/reference/generated/numpy.save.html) function.

The first argument for the function is the name/path of the file we want to save our data to. The filename/path should have a ".npy" extension. If it does not, then `np.save` will append the ".npy" extension to it.

The second argument for `np.save` is the NumPy data we want to save. The function has no return value. 

If `np.save` is called with the name of a file that already exists, it will overwrite the file.

```python
arr = np.array([1, 2, 3])
np.save('arr.npy', arr)
```

## Loading

After saving our data, we can load it again using [np.load](https://docs.scipy.org/doc/numpy/reference/generated/numpy.load.html). The function's required argument is the filename/path that contains the saved data. It returns the NumPy data exactly as it was saved.

Note that `np.load` will not append the ".npy" extension to the filename/path if it is not there.

```python
load_arr = np.load('arr.npy')
print(repr(load_arr)) # -> array([1, 2, 3])
```


