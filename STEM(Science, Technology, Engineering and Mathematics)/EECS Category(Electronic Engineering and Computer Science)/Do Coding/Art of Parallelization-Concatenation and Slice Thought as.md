# Typical APIs

# Cases

## DeepH Case

![[Pasted image 20250517161709.png]]

## `e3nn.Irreps` itself is a grand example of the thought of concatenate. 

`o3.Irreps("10x0e + 5x1o + 2x2e")`

## Graph Ops with Concatration and Slice in `e3nn`

```python
import torch
from torch_cluster import radius_graph
from torch_scatter import scatter
from e3nn import o3, nn
from e3nn.math import soft_one_hot_linspace
import matplotlib.pyplot as plt

irreps_input = o3.Irreps("10x0e + 10x1e")
irreps_output = o3.Irreps("20x0e + 10x1e")
print(f"{irreps_output.dim=}")
# create node positions
num_nodes:int = 100
pos:torch.Tensor = torch.randn(num_nodes, 3)  # random node positions

# create edges
max_radius:float = 1.8
# source and distance index tensor
edge_src, edge_dst = radius_graph(pos, max_radius, max_num_neighbors=num_nodes - 1)

print(f"{edge_src.shape=}")
print(f'{edge_dst.shape=}')
#print(f"{edge_src=}")
#print(f'{edge_dst=}')

edge_vec = pos[edge_dst] - pos[edge_src] # (num_nodes,3,)
print(f"{edge_vec.shape=}")
# compute z
num_neighbors = len(edge_src) / num_nodes
print(f"{num_neighbors=}")

f_in:torch.Tensor = irreps_input.randn(num_nodes, -1)
print(f"{f_in.shape=}")

irreps_sh:Irreps= o3.Irreps.spherical_harmonics(lmax=2)
print(f"{irreps_sh=}")
sh:torch.Tensor = o3.spherical_harmonics(irreps_sh, edge_vec, normalize=True, normalization='component') # shape (num_edges, num_basis, 9)
print(f"{sh.shape=}")

tp = o3.FullyConnectedTensorProduct(
    irreps_input, irreps_sh, irreps_output,shared_weights=False
)
print(f"{tp=} needs {tp.weight_numel=} weights")
tp.visualize()



num_basis = 5

x = torch.linspace(0.0, 2.0, 1000) # shape (x.dim,)
y = soft_one_hot_linspace( # shape (x.dim,num_basis,)
    x,
    start=0.0,
    end=max_radius,
    number=num_basis,
    basis='smooth_finite',
    cutoff=True,
)
plt.figure()
plt.plot(x, y)
print(f'{edge_vec.shape=}')
print(f'{edge_vec.norm(dim=1).shape=}')
edge_length_embedding = soft_one_hot_linspace(  # shape (num_edges,num_basis,)
    edge_vec.norm(dim=1),  # shape (num_edges,3,)->(num_edges,)
    start=0.0,
    end=max_radius,
    number=num_basis,
    basis='smooth_finite',
    cutoff=True,
)
print(f'{edge_length_embedding.shape=}')
edge_length_embedding = edge_length_embedding.mul(num_basis**0.5)
plt.figure()
print(f'{edge_vec.norm(dim=1).shape=}')
print(f'{edge_length_embedding.shape=}')
plt.scatter(edge_vec.norm(dim=1) , edge_length_embedding[:,0])
plt.scatter(edge_vec.norm(dim=1) , edge_length_embedding[:,1])

print(edge_length_embedding.shape)
edge_length_embedding.pow(2).mean()  # the second moment

fc = nn.FullyConnectedNet([num_basis, 16, tp.weight_numel], torch.relu)
weight = fc(edge_length_embedding)

print(f"{weight.shape=}")
print(f"{len(edge_src)=}", f"{tp.weight_numel=}")

# For a proper notmalization, the weights also need to be mean 0
print(weight.mean(), weight.std())  # should close to 0 and 1

summand = tp(f_in[edge_src], sh, weight)

print(f"{summand.shape=}")


f_out = scatter(summand, edge_dst, dim=0, dim_size=num_nodes)

f_out = f_out.div(num_neighbors**0.5)

print(f"{f_out.shape=}")

f_out.pow(2).mean()  # should be close to 1








def conv(f_in, pos):
    edge_src, edge_dst = radius_graph(pos, max_radius, max_num_neighbors=len(pos) - 1)
    edge_vec = pos[edge_dst] - pos[edge_src]
    sh = o3.spherical_harmonics(irreps_sh, edge_vec, normalize=True, normalization='component')
    emb = soft_one_hot_linspace(edge_vec.norm(dim=1), 0.0, max_radius, num_basis, basis='smooth_finite', cutoff=True).mul(num_basis**0.5)
    return scatter(tp(f_in[edge_src], sh, fc(emb)), edge_dst, dim=0, dim_size=num_nodes).div(num_neighbors**0.5)



```
