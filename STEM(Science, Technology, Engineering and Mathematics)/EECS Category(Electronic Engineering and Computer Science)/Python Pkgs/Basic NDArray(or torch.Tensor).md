Basic `NDArray`(N-Dimensional Array) and `torch.Tensor` are both `NDArray` actually, sharing similar ops. 

# Contraction
`@` acts as matrix multiplication for the last 2 dim, while `tensordot` and `einsum` are flexible. 
## `@` or `matmul`
`(...,M,K)@(...,K,N)->(...,M,N)`

## `tensordot`
```
A = torch.tensor([[1.0, 2.0], [3.0, 4.0]])  # Shape: (2, 2)
B = torch.tensor([[5.0, 6.0], [7.0, 8.0]])  # Shape: (2, 2)
result = torch.tensordot(A, B, dims=1)  
# Contracts last dim of A (size 2) with first dim of B (size 2)


A = torch.randn(3, 2, 5) # Shape: (3, 2, 5) 
B = torch.randn(3, 5, 4) # Shape: (3, 5, 4) 
result = torch.tensordot(A, B, dims=([2], [1])) 
# Contracts dim 2 of A (size 5) with dim 1 of B (size 5)


A = torch.randn(2, 3, 4, 5)  # Shape: (2, 3, 4, 5)
B = torch.randn(5, 4, 6, 7)  # Shape: (5, 4, 6, 7)
result = torch.tensordot(A, B, dims=([2, 3], [1, 0]))  
# Contracts dims (4,5) of A with dims (5,4) of B
```

## `einsum`
```
A = torch.tensor([[1, 2], [3, 4]])
B = torch.tensor([[5, 6], [7, 8]])
result = torch.einsum("ij,jk->ik", A, B)
# equation: str, *operands*
```


# Shape Transformation
- `view`, `continguous`
- `reshape`
- `transpose/permute`
- `squeeze/unsqueeze`
- `concatenate`
- `stack`
- `repeat`
- `split/chunk`