# ref: 
- [Chat with gemini on many topics of SpaTea](https://g.co/gemini/share/5fa753e3569b) 
	- MPS order
	- why is SpaTea many body
	- SpaTea as a MPNN module
- [[Shi-Ju Ran Compressing Neural Networks Using Tensor Networkswith Exponentially Fewer Variational Parameters]] 
	similar strategy, physics inspired neural network. 
- [[Tensor Network Representation (General)]] 
- [[DeepH-1 Deep-Learning Density Functional Theory Hamiltonian for Efficient ab initio Electronic-Structure Calculation]] **directly sum up all two body interaction as a mean field effect.**  
	 ![[Pasted image 20250512201344.png]]

# Content:
## 1. Many Body Effect
**this paper introduced Many-Body consideration into GNN arch. SpaTea is a independent module that can replace massage passing layers. MPS introduced many body entanglement.** 
![[Pasted image 20250612203219.png]] 
**steps:**
- $x_i\to \phi(x_{i}),\bar{\phi}(x_{i})$ $\mathbf{Emb\ Layer}$
- $K_{abmn}=G_{ab}^{\sigma}A_{mn}^{\sigma}(e_{ij})$ $\sigma$ is a virtual. 
- $R_{m_{0}n_{N-1}}(i)=\phi^{a}_{j=0}K_{abm_{0}n_{0}}(e_{i,j=0})\bar\phi^{b}_{j=0} \phi^{a}_{j=1}K_{ab,m_{1}=n_{0},n_{1}}(e_{i,j=1})\bar\phi^{b}_{j=1}\dots$ 
	**contraction is not summation, this take the many body effect into consideration, if any $\phi_{j}$ changed, all nodes on the contraction line are affected. this is entanglement, this is global effect, and this is many body effect.** 
- $H_{ab}(i)=R_{mn}S^{nm}_{ab}$, $S^{mn}_{ab}$ works for changing $R_{mn}$(rectangle)'s shape from $mn$ to $ab$. 
- $x_{i,a}^{t}=H_{ab}(i)\phi^{b}(x_{i}^{t-1})$ $a \neq b, a <b$ 
![[Pasted image 20250612205130.png]]  


![[Pasted image 20250528224146.png]] 
the whole module arch acts as a massage passing layer. 

# 2. Local Coordinates for invariant scalarization. 
this module just transfer these vectors into a local coordinates version scalars(or maybe arrays), just like [[DeepH-1 Deep-Learning Density Functional Theory Hamiltonian for Efficient ab initio Electronic-Structure Calculation]] but not like [[DeepH-E3 General framework for E(3)-equivariant neural network representation of density functional theory Hamiltonian]]


# SpaTea Modules: A Comprehensive Guide 📝

## 🧠 Insight and Inspiration

* **Insight**: Standard Graph Neural Networks (GNNs) often use message-passing schemes that can be viewed as "mean-field" approximations. This means they might not fully capture the complex, many-body interactions (relationships involving more than two nodes simultaneously) that are critical in many physical and geometric systems. The paper "A quantum-inspired neural network for geometric modeling" [cite: 1] posits that a more expressive method is needed to model these higher-order relationships and the inherent symmetries present in geometric graphs[cite: 1].
* **Inspiration (DMRG & Tensor Networks)**:
    * Computational physics, especially for quantum many-body systems, utilizes **Tensor Networks**, such as **Matrix Product States (MPS)**, to efficiently represent and manage very complex, high-dimensional states or operators[cite: 1]. MPS is a 1D tensor network that can effectively capture correlations and significantly reduce the exponential complexity typically associated with many-body systems[cite: 1].
    * The **Density Matrix Renormalization Group (DMRG)** algorithm is a powerful method that employs MPS to find, for example, the ground states of quantum systems[cite: 1]. A core idea in DMRG is "renormalization," where an effective Hamiltonian (an operator describing the system's energy) is defined for a part of the system by systematically incorporating the influence of the rest of the system[cite: 1, 110, 408].
    * SpaTea draws inspiration from these fundamental concepts: it uses MPS to structure the aggregation of information (both from a node's neighbors and across different layers of the network) and reflects the DMRG-like idea of forming an effective operator for a node based on its surrounding environment[cite: 1, 103, 113].

---
## 🌐 1. Spatial Aggregation Module (Equivariant MPS-based Message Passing)

This module fundamentally redefines how a node `i` aggregates information from its neighboring nodes to update its own state `x_i`[cite: 1].

* **Purpose**: To model many-body interactions within a node's immediate neighborhood more effectively than standard GNN message passing allows[cite: 1], while respecting crucial geometric symmetries (equivariance)[cite: 1, 7].
* **Inputs**:
    * Invariant features of the central node `i`: $\phi(x_i^{t-1})$ (these are features from the previous layer $t-1$)[cite: 1].
    * Invariant features of neighbor nodes $j \in N(x_i)$: $\phi(x_j^{t-1})$ and their complex conjugates $\overline{\phi}(x_j^{t-1})$[cite: 1, 150]. (These are achieved via a "scalarization" process if the original features are equivariant, meaning they change predictably with rotations/translations)[cite: 1, 143, 176].
    * Edge features $e_{ij}$ for each connection between node `i` and its neighbor `j`[cite: 1, 154].
    * The neighbors $N(x_i)$ of node `i` are typically processed in an ordered sequence, for example, sorted by their Euclidean distance to `i`[cite: 1, 159].

### Detailed Realization (Words & Formulism) 🛠️

The process effectively constructs an "effective operator" $\hat{H}_i$ for node `i` by considering its ordered neighbors[cite: 1].

* **Step 1: Edge-wise Spatial Aggregation Kernel $K(e_{ij})$**
    For each edge $e_{ij}$ connecting a neighbor $j$ to the central node `i`, a learnable "kernel" is defined[cite: 1]. This kernel is structured as a Matrix Product Operator (MPO) with one virtual leg (index $\sigma$) and four physical legs (indices $a,b,m,n$), as specified in Equation 12 of the paper[cite: 1]:
    $$K_{abmn}(e_{ij}) = \sum_{\sigma} G_{ab}^{\sigma} \cdot A_{mn}^{\sigma}(e_{ij})$$
    [cite: 1]
    * $G_{ab}^{\sigma}$: These are learnable tensor parameters that are shared across different edges[cite: 1, 158].
    * $A_{mn}^{\sigma}(e_{ij})$: This component is specific to the edge $e_{ij}$ and is parameterized, for instance, by a small neural network (often called a Hypernetwork) that takes the edge features $e_{ij}$ as its input[cite: 1, 154]. This allows the kernel to adapt dynamically to different types of edges or edge properties[cite: 1].
    * The indices $(a,b)$ are designed to contract with the feature embeddings of the neighbor node $j$, specifically $(\phi(x_j), \overline{\phi}(x_j))$[cite: 1, 154].
    * The indices $(m,n)$ are "virtual" indices that will be contracted sequentially along the chain of neighbors[cite: 1, 153, 155].

* **Step 2: Aggregating Neighbor Information $R(i)$**
    Information from the ordered sequence of neighbors of node `i` is combined by contracting their feature embeddings with their respective edge kernels $K(e_{ij})$ along the virtual indices $(m,n)$[cite: 1, 155]. This forms a rank-two tensor $R_{m_0 n_{N-1}}(i)$ which effectively summarizes the influence of the entire neighborhood[cite: 1, 155]. This process is detailed in Equation 13 of the paper[cite: 1].
    Let the ordered neighbors be $j_0, j_1, \dots, j_{N-1}$.
    $$R_{m_0 n_{N-1}}(i) = \sum_{\text{internal indices}} [\phi^a(j_0)K_{abm_0 n_0}(e_{ij_0})\overline{\phi}^b(j_0)] \cdot \dots \cdot [\phi^a(j_{N-1}) K_{abm_{N-1}n_{N-1}}(e_{ij_{N-1}}) \overline{\phi}^b(j_{N-1})]$$
    [cite: 1]
    This operation is an MPS-like contraction performed along the chain of neighbors[cite: 1]. The size of the virtual dimension for $m_k, n_k$ is $\chi$[cite: 1, 155].

* **Step 3: Forming the Effective Operator $\hat{H}_i$**
    The aggregated neighborhood information $R(i)$ is then contracted with another learnable node-specific kernel $S$ to create what the paper terms an "effective Hamiltonian" operator $\hat{H}_i$ for node `i`[cite: 1, 156]. This is shown in Equation 14[cite: 1]:
    $$\hat{H}_{ab}(i) = \sum_{m,n} R_{mn} S_{ab}^{nm}$$
    [cite: 1]
    * $S_{ab}^{nm}$: These are learnable tensor parameters that can also depend on the specific node `i` and the current layer index $t$[cite: 1, 156].

* **Step 4: Updating Node `i`'s Features**
    The new feature representation $x_i^t$ of node `i` at layer $t$ is obtained by applying the operator $\hat{H}_i$ to its feature embedding $\phi(x_i^{t-1})$ from the previous layer[cite: 1, 157]. This update rule is given by Equation 15[cite: 1]:
    $$x_i^t = \hat{H}_i(\phi(x_i^{t-1})) = \sum_{b} \hat{H}_{ab}(i) (\phi^b(x_i^{t-1}))$$
    [cite: 1]
    The output $x_i^t$ is an invariant quantity because both $\hat{H}_{ab}(i)$ and $\phi^b(x_i^{t-1})$ are constructed to be invariant under SE(3) transformations[cite: 1, 146].

* **Handling Permutation Symmetry** 🛡️
    If multiple neighbors (e.g., $x$ and $y$) are equidistant from the central node $z$, their processing order within the MPS chain is arbitrary[cite: 1, 159]. To ensure the final result is consistent and does not depend on this arbitrary choice, a commutativity condition is imposed on the $G$ tensors associated with these neighbors, as outlined in Equation 16[cite: 1, 160, 161]:
    $$G_{ab}^{\sigma}(x) = U \text{diag}(x) U^* \quad \text{and} \quad G_{bc}^{\sigma'}(y) = U \text{diag}(y) U^*$$
    [cite: 1]
    This means the $G$ matrices for these specific neighbors are simultaneously diagonalizable by the same unitary transformation $U$[cite: 1, 161].

### Pseudocode for Spatial Aggregation (Conceptual) 💻

```pseudocode
function Spatial_Aggregation_SpaTea(node_i, neighbors_of_i, prev_layer_features, edge_features, model_parameters):
  // Ensure input features for node_i are invariant (scalarized if necessary) 
  phi_i_prev = get_invariant_embedding(prev_layer_features[node_i]) // Concept of scalarization [cite: 1, 143]

  // Order neighbors, e.g., by distance to node_i [cite: 1, 159]
  ordered_neighbors = sort_neighbors(neighbors_of_i, node_i) 

  // Initialize an aggregated tensor R for the start of the MPS chain
  current_R_tensor = identity_tensor_for_mps_start 

  for neighbor_j in ordered_neighbors:
    edge_ij = edge_features[node_i, neighbor_j]
    phi_j_prev = get_invariant_embedding(prev_layer_features[neighbor_j]) // Get invariant features [cite: 1, 149]
    phi_j_bar_prev = conjugate(phi_j_prev) // Use conjugate features [cite: 1, 150]

    // Step 1: Get Edge-wise Kernel K (based on Eq. 12 [cite: 1])
    A_mn_sigma_ij = model_parameters.HyperNet_A(edge_ij) // A(e_ij) from Hypernet [cite: 1, 154]
    G_ab_sigma = model_parameters.G_spatial // G are tensor parameters [cite: 1, 158]
    K_abmn_ij = sum_over_sigma (G_ab_sigma * A_mn_sigma_ij) // Definition of K [cite: 1]

    // Step 2: Contract to build R(i) tensor sequentially (conceptual view of Eq. 13 [cite: 1])
    current_R_tensor = contract_mps_step(current_R_tensor, K_abmn_ij, phi_j_prev, phi_j_bar_prev)
  
  R_i_final = current_R_tensor // This represents R_m0nN-1(i) from Eq. 13 [cite: 1]

  // Step 3: Form Effective Operator H_i (based on Eq. 14 [cite: 1])
  S_ab_nm = model_parameters.S_node_kernel // S is a node kernel [cite: 1, 156]
  H_ab_i = sum_over_mn (R_i_final_mn * S_ab_nm) // Definition of H_hat [cite: 1]

  // Step 4: Update Node i's Features (based on Eq. 15 [cite: 1])
  x_i_new_invariant = sum_over_b (H_ab_i * phi_i_prev_b) // Update rule [cite: 1]
  
  return x_i_new_invariant
```

## ⏳ 2. Temporal Aggregation Module (MPS-based Layer Aggregation)

This module is responsible for combining the representations of a specific node `n` that have been generated from _all preceding layers_ of the GNN.

- **Purpose**: To construct a rich, hierarchical representation for each node that effectively captures information from different levels of abstraction that are processed by the successive layers of the network. Standard GNNs might simply use the output of the final layer or a basic sum/concatenation of layer outputs.
    
- **Inputs**:
    - Initial node embedding $v_n^0$ (e.g., a one-hot encoding representing the node type).
        
    - Node representations $x_n^l$ for node $n$ obtained from each layer $l=0, \dots, L-1$. (Here, $x_n^0$ could be $v_n^0$, and $x_n^l$ for $l>0$ is the output from the spatial aggregation module and any subsequent node updates for layer $l$).
        

### Detailed Realization (Words & Formulism) 🛠️

- **Iterative Update using a Residual MPS (aResMPS) (Equation 9)** The aggregated representation $v_{na_{l+1}}^{l+1}$ for node $n$ that incorporates information up to layer $l+1$ is defined iteratively, as specified in Equation 9 of the paper: $$v_{na_{l+1}}^{l+1} = v_{na_l}^l + \sigma \left( \sum_{a_l s_l} v_{na_l}^l x_{ns_l}^l \frac{\phi_{a_l s_l a_{l+1}}^l}{Z(l)} + b_{a_{l+1}}^l \right)$$
    
    - $v_{na_l}^l$: This is the aggregated representation of node $n$ having processed information up to layer $l$. The index $a_l$ is a virtual index of the MPS structure.
        
    - $x_{ns_l}^l$: This is the node representation of node $n$ coming from layer $l$ (i.e., the output of the spatial aggregation for that layer). The index $s_l$ is the feature index.
        
    - $\phi_{a_l s_l a_{l+1}}^l$: This is a learnable 3rd-order tensor specific to layer $l$. It forms the core of the MPO that contracts the previously aggregated state $v^l$ with the new information $x^l$ from the current layer to produce the update. $a_l, a_{l+1}$ are virtual bond indices, and $s_l$ is the physical index corresponding to $x^l$.
        
    - $b_{a_{l+1}}^l$: This is a learnable bias term for layer $l$.
        
    - $Z(l) := || x_{ns_l}^l \phi_{a_l s_l a_{l+1}}^l ||$: This is a normalization factor designed to maintain the scale of the aggregation and improve stability.
        
    - $\sigma$: A non-linear activation function (e.g., ReLU, SiLU).
        
    - The final output of this temporal aggregation process for node $n$ after $L$ layers would be $v_{na_L}^L$, which the paper denotes as $\Psi(v_n^0, x_n^1, \dots, x_n^L)$. This resulting quantity is SE(3) invariant if all the input layer representations $x_n^l$ are themselves invariant.
        

### Pseudocode for Temporal Aggregation (Conceptual) 💻
```
function Temporal_Aggregation_SpaTea(initial_node_embedding_v0, list_of_layer_outputs_x_l, model_parameters, num_layers_L):
  // list_of_layer_outputs_x_l should contain [x_node_from_layer_0, ..., x_node_from_layer_L-1]
  // where x_node_from_layer_l is the invariant output for the node from the spatial aggregation of layer l
  
  v_aggregated_prev = initial_node_embedding_v0 // This represents v^0 [cite: 1, 117]

  for l from 0 to num_layers_L-1: // Iterate for each layer's output
    x_current_layer_output = list_of_layer_outputs_x_l[l] // This is x_ns_l^l [cite: 1, 117]

    // Retrieve learnable MPS tensor (phi^l) and bias (b^l) for this aggregation step from model_parameters
    phi_tensor_l = model_parameters.get_temporal_MPS_tensor(layer_index = l) // This is phi_a_l s_l a_l+1^l [cite: 1, 118]
    bias_l = model_parameters.get_temporal_bias(layer_index = l) // This is b_a_l+1^l [cite: 1, 118]

    // Calculate normalization factor Z(l) (as in Eq. 9 [cite: 1])
    // Note: Actual norm calculation might be more involved
    Z_l = norm_for_stabilization(x_current_layer_output, phi_tensor_l) // Normalizing factor [cite: 1, 120]

    // Core MPS contraction and update step (as in Eq. 9 [cite: 1])
    // This sum is over previous virtual index a_l and physical index s_l from x_current_layer_output
    update_term_contracted = contract_sum_temporal(v_aggregated_prev, x_current_layer_output, phi_tensor_l / Z_l)
    
    update_term_with_bias = update_term_contracted + bias_l // Adding bias [cite: 1]
    activated_update = activation_function_sigma(update_term_with_bias) // Activation [cite: 1, 118]

    // The residual connection is inherent in the formulation v_prev + update (as in Eq. 9 [cite: 1])
    v_aggregated_current = v_aggregated_prev + activated_update 
    
    v_aggregated_prev = v_aggregated_current // Update for the next iteration
    
  return v_aggregated_current // This is the final hierarchical node representation
```