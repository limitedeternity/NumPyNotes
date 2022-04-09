## Arithmetic

One of the main purposes of NumPy is to perform multi-dimensional arithmetic. Using NumPy arrays, we can apply arithmetic to each element with a single operation.

```python
arr = np.array([[1, 2], [3, 4]])
print(repr(arr + 1)) # -> array([[2, 3], [4, 5]])
print(repr(arr - 1.2)) # -> array([[-0.2, 0.8], [1.8, 2.8]])
print(repr(arr * 2)) # -> array([[2, 4], [6, 8]])
print(repr(arr / 2)) # -> array([[0.5, 1.], [1.5, 2.]])
print(repr(arr // 2)) # -> array([[0, 1], [1, 2]])
print(repr(arr**2)) # -> array([[1, 4], [9, 16]])
print(repr(arr**0.5)) # -> array([[1., 1.41421356], [1.73205081, 2.]])
```

Using NumPy arithmetic, we can easily modify large amounts of numeric data with only a few operations. For example, we could convert a dataset of Fahrenheit temperatures to their equivalent Celsius form.

```python
def f2c(temps):
  return (5/9)*(temps-32)

fahrenheits = np.array([32, -4, 14, -40])
celsius = f2c(fahrenheits)
print(repr(celsius)) # -> array([  0., -20., -10., -40.])
```

## Non-linear functions

Apart from basic arithmetic operations, NumPy also allows you to use non-linear functions such as exponentials and logarithms.

The function [np.exp](https://docs.scipy.org/doc/numpy/reference/generated/numpy.exp.html) performs a base *e* exponential on an array, while the function [np.exp2](https://docs.scipy.org/doc/numpy/reference/generated/numpy.exp2.html) performs a base 2 exponentiation. Likewise, [np.log](https://docs.scipy.org/doc/numpy/reference/generated/numpy.log.html), [np.log2](https://docs.scipy.org/doc/numpy/reference/generated/numpy.log2.html), and [np.log10](https://docs.scipy.org/doc/numpy/reference/generated/numpy.log10.html) all compute logarithms on an input array, using base *e*, base 2, and base 10, respectively.

To do a regular power operation with any base, we use [np.power](https://docs.scipy.org/doc/numpy/reference/generated/numpy.power.html). The first argument of the function is the base, while the second is the power. If the base or power is an array rather than a single number, the operation is applied to every element in the array.

```python
arr = np.array([[1, 2], [3, 4]])
print(repr(np.power(3, arr))) # -> array([[3, 9], [27, 81]])

arr2 = np.array([[10.2, 4], [3, 5]])
print(repr(np.power(arr2, arr))) # -> array([[10.2, 16. ], [27., 625.]])
```

## Matrix multiplication

Since NumPy arrays are basically vectors and matrices, it makes sense that there are functions for dot products and matrix multiplication. Specifically, the main function to use is [np.matmul](https://docs.scipy.org/doc/numpy/reference/generated/numpy.matmul.html), which takes two vector/matrix arrays as input and produces a dot product or matrix multiplication.

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([-3, 0, 10])
print(np.matmul(arr1, arr2)) # -> 27

arr3 = np.array([[1, 2], [3, 4], [5, 6]])
arr4 = np.array([[-1, 0, 1], [3, 2, -4]])
print(repr(np.matmul(arr3, arr4))) # -> array([[5, 4, -7], [9, 8, -13], [13, 12, -19]])
```
