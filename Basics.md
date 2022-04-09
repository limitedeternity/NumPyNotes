## Ranged data

While `np.array` can be used to create any array, it is equivalent to hardcoding an 
array. This won't work when the array has hundreds of values. Instead, 
NumPy provides an option to create ranged data arrays using [np.arange](https://docs.scipy.org/doc/numpy/reference/generated/numpy.arange.html). The function acts very similar to the `range` function in Python, and will always return a 1-D array.

Like `np.array`, `np.arange` performs upcasting. It also has the `dtype` keyword argument to manually cast the array.

To get evenly spaced numbers over a specified interval, we can use the [np.linspace](https://docs.scipy.org/doc/numpy/reference/generated/numpy.linspace.html) function:

```python
print(repr(np.linspace(5, 11, num=4))) # -> array([ 5.,  7.,  9., 11.])
```

## Reshaping data

The function we use to reshape data in NumPy is [np.reshape](https://docs.scipy.org/doc/numpy/reference/generated/numpy.reshape.html).
It takes in an array and a new shape as required arguments. The new shape must exactly contain all the elements from the input array. For example, we could reshape an array with 12 elements to `(4, 3)`, but we can't reshape it to `(4, 4)`.

We are allowed to use the special value of -1 in at most one dimension of the new shape. The dimension with -1 will take on the value necessary to allow the new shape to contain all the elements of the array.

```python
reshaped_arr = np.reshape(np.arange(8), (2, 4))
print(repr(reshaped_arr)) # -> array([[0, 1, 2, 3], [4, 5, 6, 7]])
print(reshaped_arr.shape) # -> (2, 4)

reshaped_arr = np.reshape(np.arange(8), (-1, 2, 2))
print(repr(reshaped_arr)) # -> array([[[0, 1], [2, 3]], [[4, 5], [6, 7]]])
print(reshaped_arr.shape) # -> (2, 2, 2)
```

While the `np.reshape` function can perform any reshaping utilities we need, NumPy provides an inherent function for flattening an array. Flattening an array reshapes it into a 1D array. Since we need  to flatten data quite often, it is a useful function.

```python
flattened = np.reshape(np.arange(8), (2, 4)).flatten()
print(repr(flattened)) # -> array([0, 1, 2, 3, 4, 5, 6, 7])
print(flattened.shape) # -> (8,)
```

## Transposing

Similar to how it is common to reshape data, it is also common to transpose data. Perhaps we have data that's supposed to be in a particular format, but some new 
data we get is rearranged. We can just transpose the data, using the [np.transpose](https://docs.scipy.org/doc/numpy/reference/generated/numpy.transpose.html) function, to convert it to the proper format.

```python
arr = np.reshape(np.arange(8), (4, 2))
transposed = np.transpose(arr)
print(arr.shape) # -> (4, 2)
print(transposed.shape) # -> (2, 4)
```

The function takes in a required first argument, which will be the array we want to transpose. It also has a single keyword argument called `axes`, which represents the new *permutation* of the dimensions.

The permutation is a tuple/list of integers, with the same length as the number of dimensions in the array. It tells us where to switch up the dimensions. For example, if the permutation had 3 at index 1, it means the old third dimension of the data becomes the new second dimension (since index 1 represents the second dimension).

```python
arr = np.reshape(np.arange(24), (3, 4, 2)))
transposed = np.transpose(arr, axes=(1, 2, 0))
print(arr.shape) # -> (3, 4, 2)
print(transposed.shape) # -> (4, 2, 3)
```

## Zeros and ones

Sometimes, we need to create arrays filled solely with 0 or 1. For example, since binary data is labeled with 0 and 1, we may need to create dummy datasets of strictly one label. For creating these arrays, NumPy provides the functions [np.zeros](https://docs.scipy.org/doc/numpy/reference/generated/numpy.zeros.html) and [np.ones](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ones.html).
They both take in the same arguments, which includes just one required argument, the array shape. The functions also allow for manual casting using the `dtype` keyword argument.

```python
arr = np.zeros(4)
print(repr(arr)) # -> array([0., 0., 0., 0.])

arr = np.ones((2, 3), dtype=np.int32)
print(repr(arr)) # -> array([[1, 1, 1], [1, 1, 1]], dtype=int32)
```

If we want to create an array of 0's or 1's with the same shape and type as another array, we can use [np.zeros_like](https://docs.scipy.org/doc/numpy/reference/generated/numpy.zeros_like.html) and [np.ones_like](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ones_like.html).

```python
arr = np.array([[1, 2], [3, 4]])
print(repr(np.zeros_like(arr))) # -> array([[0, 0], [0, 0]])

arr = np.array([[0., 1.], [1.2, 4.]])
print(repr(np.ones_like(arr))) # -> array([[1., 1.], [1., 1.]])
```
