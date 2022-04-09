## Random integers

Similar to the Python `random` module, NumPy has its own submodule for pseudo-random number generation called `np.random`. It provides all the necessary randomized operations and extends it to multi-dimensional arrays. To generate pseudo-random integers, we use the [np.random.randint](https://docs.scipy.org/doc/numpy-1.14.0/reference/generated/numpy.random.randint.html#numpy.random.randint) function.

The `np.random.randint` function takes in a single required argument, which actually depends on the `high` keyword argument.

If `high is None` (which is the default value), then the required argument represents the upper (exclusive) end of the range, with the lower end being 0. Specifically, if the required argument is *n*, then the random integer is chosen uniformly from the range [0, *n*).

If `high is not None`, then the required argument will represent the lower (inclusive) end of the range, while `high` will represent the upper (exclusive) end.

The `size` keyword argument specifies the size of the output array, where each 
integer in the array is randomly drawn from the specified range. As a default, `np.random.randint` returns a single integer.

```python
print(np.random.randint(5)) # -> 4
print(np.random.randint(5, high=6)) # -> 5

random_arr = np.random.randint(-3, high=14, size=(2, 2))
print(repr(random_arr)) # -> array([[13, 6], [1, -3]])
```

## Utility functions

Some fundamental utility functions from the `np.random` module are [np.random.seed](https://docs.scipy.org/doc/numpy-1.14.0/reference/generated/numpy.random.seed.html#numpy.random.seed) and [np.random.shuffle](https://docs.scipy.org/doc/numpy-1.14.0/reference/generated/numpy.random.shuffle.html#numpy.random.shuffle). We use the `np.random.seed` function to set the [random seed](https://en.wikipedia.org/wiki/Random_seed), which allows us to control the outputs of the pseudo-random functions. The function takes in a single integer as an argument, representing the random seed.

```python
np.random.seed(1)
print(np.random.randint(10)) # -> 5
random_arr = np.random.randint(3, high=100, size=(2, 2))
print(repr(random_arr)) # -> array([[15, 75], [12, 78]])

# New seed
np.random.seed(2)
print(np.random.randint(10)) # -> 8
random_arr = np.random.randint(3, high=100, size=(2, 2))
print(repr(random_arr)) # -> array([[18, 75], [25, 46]])

# Original seed
np.random.seed(1)
print(np.random.randint(10)) # -> 5
random_arr = np.random.randint(3, high=100, size=(2, 2))
print(repr(random_arr)) # -> array([[15, 75], [12, 78]])
```

The `np.random.shuffle` function allows us to randomly shuffle an array. Note that the shuffling happens in place (i.e. no return value), and shuffling multi-dimensional arrays only shuffles the first dimension.

```python
vec = np.array([1, 2, 3, 4, 5])
np.random.shuffle(vec)
print(repr(vec)) # -> array([4, 1, 3, 2, 5])

matrix = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
np.random.shuffle(matrix)
print(repr(matrix)) # -> array([[4, 5, 6], [7, 8, 9], [1, 2, 3]])
```

## Distributions

Using `np.random` we can also draw samples from probability distributions. For example, we can use [np.random.uniform](https://docs.scipy.org/doc/numpy-1.14.0/reference/generated/numpy.random.uniform.html#numpy.random.uniform) to draw pseudo-random real numbers from a [uniform distribution](https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)).

The function `np.random.uniform` actually has no required arguments. The keyword arguments, `low` and `high`, represent the inclusive lower end and exclusive upper end from which to draw random samples. Since they have default values of 0.0 and 1.0, 
respectively, the default outputs of `np.random.uniform` come from the range [0.0, 1.0).

The `size` keyword argument is the same as the one for `np.random.randint`, i.e. it represents the output size of the array.

```python
print(np.random.uniform()) # -> 0.8973168137915013
print(np.random.uniform(low=-1.5, high=2.2)) # -> 1.0571472229621444
print(repr(np.random.uniform(size=3))) # -> array([0.23337496, 0.5781942, 0.50841461])
print(repr(np.random.uniform(low=-3.4, high=5.9, size=(2, 2)))) # -> array([[-0.01932957, 3.73228525], [2.14449871, -1.28905229]])
```

Another popular distribution we can sample from is the [normal (Gaussian) distribution](https://en.wikipedia.org/wiki/Normal_distribution). The function we use is [np.random.normal](https://docs.scipy.org/doc/numpy-1.14.0/reference/generated/numpy.random.normal.html#numpy.random.normal).

```python
print(np.random.normal()) # -> -0.5405712424148714
print(np.random.normal(loc=1.5, scale=3.5)) # -> 3.921373129763735
print(repr(np.random.normal(loc=-2.4, scale=4.0, size=(2, 2)))) # -> array([[-6.66365691, -5.12560553], [-5.11159042, -4.62444088]])
```

Like `np.random.uniform`, `np.random.normal` has no required arguments. The `loc` and `scale` keyword arguments represent the mean and standard deviation, respectively, of the normal distribution we sample from.

## Custom sampling

While NumPy provides built-in distributions to sample from, we can also sample from a custom distribution with the [np.random.choice](https://docs.scipy.org/doc/numpy-1.14.0/reference/generated/numpy.random.choice.html#numpy.random.choice) function.

The required argument for `np.random.choice` is the custom distribution we sample from. The `p` keyword argument denotes the probabilities given to each element in the input distribution. Note that the list of probabilities for `p` must sum to 1. When `p` is not set, the probabilities are equal for each element in the distribution (and sum to 1).

```python
colors = ['red', 'blue', 'green']
print(np.random.choice(colors)) # -> blue
print(repr(np.random.choice(colors, size=2))) # -> array(['red', 'blue'], dtype='<U5')
print(repr(np.random.choice(colors, size=(2, 2), p=[0.8, 0.19, 0.01]))) # -> array([['blue', 'red'], ['red', 'red']], dtype='<U5')
```
