
# Repo Arch of DeepH-1
by analyse its import realtion, i can sketch a graph of this repo. 
![[Pasted image 20250516113341.png]]  
I forcily categorize these modules into a layered arch regime. 
it's incorrect to name the kernel(who manage all hardwares from its original meaning in operating system realm) a user interface layer. but anyway, i have done this. 

it's nice to see that the main body is just `model.py`. it consist of only a small ratio of the whole repo. 


# Main Body `model.py` 

## main body of main body `HGNN:class`
**to specify all inputs, outputs and apis**. 
especifically to specify their **type, shape and role**. 

```
embed:Embedding(
species:int,
)->atom_fea:(len_in_atom_fea)
one-hot emb atom fea
```

```
distance_expansion:GaussianBasis(
distance:float,
)->edge_fea:(len_distance_expansion)
distance emb edge fea
```

```
MPLayer:
```
- ```embed: one-hot, species_atom:int->atom_feature:(len_in_atom_feature)```
- `distance_eppansion:GaussianBasis ->edge_fea:(len_in_edge_fea)`








