## Arrays

NumPy arrays are basically just Python lists with added features. In fact, you can easily convert a Python list to a Numpy array using the `np.array` function, which takes in a Python list as its required argument. The function also has quite a few keyword arguments, but the main one to know is `dtype`. The `dtype` keyword argument takes in a [NumPy type](https://docs.scipy.org/doc/numpy/user/basics.types.html) and manually casts the array to the specified type.

When the elements of a NumPy array are mixed types, then the array's type will be *upcast* to the highest level type. This means that if an array input has mixed `int` and `float` elements, all the integers will be cast to their floating-point equivalents. If an array is mixed with `int`, `float`, and `string` elements, everything is cast to strings.

## Copying

Similar to Python lists,  when we make a reference to a NumPy array it doesn't create a different  array. Therefore, if we change a value using the reference variable, it  changes the original array as well. We get around this by using an  array's inherent `copy` function. The function has no required arguments, and it returns the copied array.

## Casting

We cast NumPy arrays through their inherent `astype` function. The function's required argument is the new type for the array. It returns the array cast to the new type.

## NaN

When we don't want a NumPy array to contain a value at a particular index, we can use `np.nan` to act as a placeholder. A common usage for `np.nan` is as a filler value for incomplete data. Note that `np.nan` cannot take on an integer type.

## Infinity

To represent infinity in NumPy, we use the `np.inf` special value. We can also represent negative infinity with `-np.inf`. Note that `np.inf` cannot take on an integer type.