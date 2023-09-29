## Tensors

>[!definition]
>**Tensors** are machine learning–optimized arrays.

>[!hint]
>**Never** use for loops.

### Construction

From arrays:
```python
data = [[1, 2], [3, 4]]
x_data = torch.tensor(data)
```

From numpy array:
```python
np_array = np.array(data)
x_data = torch.tensor(np_array)
```

Random, 1s, and 0s:
```python
shape = (2, 3,)
rand_tensor = torch.rand(shape)
ones_tensor = torch.ones(shape)
zeros_tensor = torch.zeros(shape)
```

### Operations

Multiplication
```Python
a = torch.randn(3)
torch.mul(a, 100)
```

Addition
```Python
a = torch.randn(3)
torch.add(a, 100)
```

Matrix multiplication
```Python
a = torch.randn(3, 4)
b = torch.randn(4)
torch.mul(a, b)
```

Broadcasting

$$\begin{bmatrix}
1 & 2 \\3 & 4 \\5 & 6
\end{bmatrix} + \begin{bmatrix}10 & 20\end{bmatrix}\rightarrow\begin{bmatrix}
1 & 2 \\3 & 4 \\5 & 6
\end{bmatrix}+\begin{bmatrix}10 & 20 \\ 10& 20 \\ 10& 20\end{bmatrix}$$

```python
x = torch.empty(5, 1, 4, 1)
y = torch.empty(3, 1, 1)
(x + y).size() 
# == [5, 3, 4, 1]
```

If the dimensions of `x` and `y` aren't equal, PyTorch prepends 1 to the dimensions of the smaller matrix to make them equal length. 
### Indexing

Indexing for tensors is like array indexing.

```python
x = torch.tensor(...)
x[0]
x[0][1]
```

### Slicing
$$t[a:b]=[t_a, t_{a+1}, \dots, \underbrace{t_{b-1}}_{\mathclap{\text{exclusive}}}]$$
```python
tensor[a:b]  # Values with index [a..b - 1]
tensor[:b]  # Select all before b - 1
```

If we have one row
$$t[:1,1]=t[0:,1]=t[0:1,1]$$
### Filtering

`torch.where(condition, x, y)` searches a boolean tensor `condition`. If the element is true, it returns the corresponding value in the tensor `x`, otherwise `y`.

### Attributes

- Dimensions: `tensor.shape`
- Datatype: `tensor.dtype`
- Device (e.g., GPUs): `tensor.device`

## Code Design

### Vectorization

>[!definition]
>**Vectorization** is implementing functions using matrix operations. 

Vectorization allows us to run operations in parallel, speeding things up.

