# Ref:
- [[Code Review of DeepH-1]]
- [[Basic DFT]] 

# Contents: 
## 1. Arch
Here we develop a deep neural network approach to represent DFT Hamiltonian (DeepH) of crystalline materials, aiming to ***bypass* the computationally demanding self-consistent field iterations of DFT and substantially *improve* the efficiency of ab initio electronic-structure calculations**.

DeepH adopt deep neural network to consruct DFT Hamiltonian $H_{\mathrm{DFT}}$. 

one key feature of DeepH is **covariant** while using neural network. 
[**citation 27  Tensor field network  rotation and translational equivariant nn for 3d point cloud.** ](https://arxiv.org/abs/1802.08219) 

$H_{\mathrm{DFT}}$ is covariant via using local basis and local coordinate and local transform. 
**DeepH** gives a method to address the gauge covariant issue and large dimensionality, variables quantity issue. 
>The challenging issues related to the (infinitely) large dimensionality and gauge (or rotation) covariance of the DFT Hamiltonian matrix are solved by virtue of locality, including the use of the local coordinate, local basis transformation and localized orbitals as basis functions.

![[Pasted image 20250512111712.png]]

**DeepH** employed local atom-orbital like basis to ensure sparsity of the $H_{\mathrm{DFT}}$. 
**DeepH** arch is below.  
![[Pasted image 20250512162721.png]] 
 ![[Pasted image 20250512201344.png]]
where $z_{ik}= v_{i}||v_{k}||e_{ik}$. 

 ![[Pasted image 20250512201442.png]]
 
DeepH employ local coordinate and then DFT hamiltionian $H_{\mathrm{DFT}}\  \mathrm{or} \ H_{ij}$becomes $H_{ij}'$, whose shape under a atom orbital like basis would be $H'_{i\alpha,j\beta}$.  
Loss func is MAE of $H'_{i\alpha,j\beta}$.

## 2. Concrete Steps of DeepH
[Steps of DeepH with Gemini](https://g.co/gemini/share/9988674cfbfd) 
> By gemini 2.5pro 
> The architecture generally consists of:
> 
> 1. Initial embedding.
> 2. L−1 Message Passing (MP) layers. The paper mentions using 5 MP layers (Source 83), so L−1=5.
> 3. One final Local Coordinate Message Passing (LCMP) layer. This would be layer L.
> 
> **Step 0: Initial Features**
> 
> - **vi(0)​ (Initial Vertex Feature for atom i)**
>     
>     - **Mapping (Source 71, Eq. 1):** vi(0)​=Embedding(Zi​)
>     - **Shape:** 64 dimensions. (Source 261: "The dimension of elemental embeddings... is set to 64.")
>     - **Meaning:** A learned vector representation (embedding) of the atomic species of atom i, derived from its atomic number Zi​. This vector encodes the type of atom.
> - **eij(0)​ (Initial Edge Feature for edge between atom i and j)**
>     
>     - **Mapping (Source 71, Eq. 2 & Source 261):** This is a vector where each component is calculated as gn​=exp(−(∣rij​∣−rn​)2/σ2) for a set of NRBF​ different distance centers rn​. Here ∣rij​∣ is the interatomic distance.
>     - **Shape:** 128 dimensions. (Source 261: "The initial edge features are a set of 128 Gaussian functions...")
>     - **Meaning:** A feature vector representing the interatomic distance ∣rij​∣. This is a Radial Basis Function (RBF) expansion, which provides a rich, smooth encoding of the distance, rather than just the scalar value. Each of the 128 components responds to how close ∣rij​∣ is to one of the 128 predefined distance centers (rn​).
> 
> ---
> 
> **Step l (for l=1,...,L−1): Message Passing (MP) Layers** (The paper uses L−1=5 MP layers)
> 
> - **Mapping to vi(l)​ (Vertex Update at layer l) (Source 72, Eq. 3):**
>     
>     1. **Prepare messages:** For each neighbor k of atom i (denoted k∈Ni​):
>         - Concatenate features from the previous layer (l−1): zik(l−1)​=vi(l−1)​∣∣vk(l−1)​∣∣eik(l−1)​
>             - vi(l−1)​ (shape 64)
>             - vk(l−1)​ (shape 64)
>             - eik(l−1)​ (shape 128, from atom i to neighbor k)
>             - Shape of zik(l−1)​: 64+64+128=256 dimensions.
>         - Transform zik(l−1)​ using a neural network Φv(l)​ to get a message mik(l)​=Φv(l)​(zik(l−1)​). (This Φv(l)​ is detailed in Source 241, and it maps its input to a 64-dimensional message to match vertex feature dimensionality).
>     2. **Aggregate messages:** Sum messages from all neighbors: Mi(l)​=∑k∈Ni​​mik(l)​ (Shape: 64 dimensions).
>     3. **Update vertex feature:** vi(l)​=LayerNorm(Mi(l)​)+vi(l−1)​ (Residual connection and normalization).
> - **vi(l)​ (Vertex Feature at MP layer l)**
>     
>     - **Shape:** 64 dimensions. (Source 261: "...vertex feature vectors in each layer, is set to 64.")
>     - **Meaning:** An updated embedding for atom i. It now incorporates information from its direct (1-hop) neighbors and the edges connecting to them from layer l−1. After l layers, it implicitly contains information from its l-hop neighborhood.
> - **Mapping to eij(l)​ (Edge Update at layer l) (Source 72, Eq. 4):**
>     
>     1. **Prepare input:** Concatenate the newly updated vertex features of atoms i and j at layer l, and the edge feature from the previous layer (l−1): xij(l)​=vi(l)​∣∣vj(l)​∣∣eij(l−1)​
>         - vi(l)​ (shape 64)
>         - vj(l)​ (shape 64)
>         - eij(l−1)​ (shape 128)
>         - Shape of xij(l)​: 64+64+128=256 dimensions.
>     2. **Update edge feature:** Transform xij(l)​ using a neural network Φe(l)​: eij(l)​=Φe(l)​(xij(l)​). (This Φe(l)​ is detailed in Source 241 and is designed to output a 128-dimensional vector).
> - **eij(l)​ (Edge Feature at MP layer l)**
>     
>     - **Shape:** 128 dimensions. (Source 262: "The edge feature vector in each layer is a 128-dimensional vector.")
>     - **Meaning:** An updated embedding for the edge (i,j). It now incorporates information from the updated states of the atoms i and j it connects (at layer l) and its own state from the previous layer.
> 
> ---
> 
> **Step L: Local Coordinate Message Passing (LCMP) Layer** (The 6th layer in the 5+1 setup) The notation here refers to the local coordinate system defined for the specific edge ij whose Hamiltonian block Hij′​ is being predicted.
> 
> - **Mapping to vi(L)​ (LCMP Vertex Update, denoted viij(L)​ in paper for context of edge ij) (Source 78, Eq. 5):**
>     
>     1. **Prepare messages:** For each neighbor k of atom i:
>         - Get zik(L−1)​=vi(L−1)​∣∣vk(L−1)​∣∣eik(L−1)​ (Shape: 256, from the last MP layer).
>         - Get orientation information: unit vector r^ikij​ (of bond ik relative to the local coordinate defined for target edge ij). This is expanded using 25 real spherical harmonic functions {Ylm​(θikij​,ϕikij​)} (Source 78, 79, 263). Shape of {Ylm​} vector: 25.
>         - Concatenate: yikij(L−1)​=zik(L−1)​∣∣{Ylm​(θikij​,ϕikij​)} (Shape: 256+25=281).
>         - Transform yikij(L−1)​ using a neural network Φv(L)​ to get a message mikij(L)​=Φv(L)​(yikij(L−1)​). (This Φv(L)​ maps its input to a 64-dimensional message).
>     2. **Aggregate messages:** Sum messages from all neighbors: Miij(L)​=∑k∈Ni​​mikij(L)​ (Shape: 64 dimensions).
>     3. **Set vertex feature for LCMP edge update:** vi(L)​=Miij(L)​ (Note: Eq. 5 in the paper doesn't show a residual for this specific vertex feature used in the LCMP edge update).
> - **vi(L)​ (Vertex Feature for LCMP layer, specific to the context of predicting Hij′​)**
>     
>     - **Shape:** 64 dimensions (assumed, to feed into the edge update consistently).
>     - **Meaning:** A feature vector for atom i that is now sensitive to the specific local coordinate system of the target edge ij. It incorporates explicit orientation information of its neighbors relative to this ij frame.
> - **Mapping to eij(L)​ (LCMP Edge Update, this becomes Hij′​) (Source 78, Eq. 6):**
>     
>     1. **Prepare input:** Concatenate the LCMP-contextualized vertex features vi(L)​ and vj(L)​, and the edge feature eij(L−1)​ from the last MP layer: xij(L)​=vi(L)​∣∣vj(L)​∣∣eij(L−1)​
>         - vi(L)​ (shape 64)
>         - vj(L)​ (shape 64)
>         - eij(L−1)​ (shape 128)
>         - Shape of xij(L)​: 64+64+128=256 dimensions.
>     2. **Update edge feature (predict Hij′​):** Transform xij(L)​ using a final neural network Φe(L)​: eij(L)​=Φe(L)​(xij(L)​). The crucial difference here is that the output dimension of Φe(L)​ is not 128. It is Norb,i​×Norb,j​ (number of orbitals on atom i times number of orbitals on atom j).
> - **eij(L)​ (Final Edge Feature from LCMP layer, representing Hij′​)**
>     
>     - **Shape:** Norb,i​×Norb,j​. For a Carbon-Carbon edge (13 orbitals each, as per Source 82), this shape is 13×13=169 dimensions.
>     - **Meaning:** This vector is the **flattened representation of the Hamiltonian matrix block Hij′​** in the local coordinate system defined for the edge (i,j). Each element in this vector corresponds to a specific Hiα,jβ′​ interaction energy between an orbital α on atom i and an orbital β on atom j (according to a predefined, fixed ordering of orbitals). This is the direct output from the graph neural network part that will be used to construct the physical Hamiltonian.
> 
> ---
> 
> **Final Output Transformation (Post-MPNN):**
> 
> 1. **Reshape eij(L)​:** The Norb,i​×Norb,j​-dimensional vector eij(L)​ is reshaped into an Norb,i​×Norb,j​ matrix. This matrix is Hij′​.
> 2. **Rotation to Global Coordinates (Source 80):** Hij′​ (which is in the local coordinate system) is transformed back to the global coordinate system using the appropriate rotation matrices Uij​ derived from the definition of the local coordinates: Hij​=Uij​Hij′​UijT​. The elements (Hij​)αβ​ are the final Hiα,jβ​ values.

Pesudo code
```
// --- Constants & Hyperparameters ---
DIM_V_NODE = 64          // Dimension for vertex features (both initial embedding and in MP layers)
DIM_E_EDGE_MP = 128      // Dimension for edge features in initial and MP layers
NUM_RBF_CENTERS = 128  // Number of Gaussian functions for RBF distance expansion
DIM_SPHERICAL_HARMONICS = 25 // Dimension of orientation features (Y_lm expansion)
NUM_MP_LAYERS = 5      // Number of standard Message Passing layers

// --- Input Data ---
// atoms: List of atom objects. Each atom has .id, .atomic_number, .position
// relevant_edges: List of edge tuples (atom_i, atom_j) for which H_ij needs computation
//                 (e.g., pairs within a cutoff radius Rc)
// Rc_cutoff: Distance cutoff for finding neighbors in graph construction

// --- Data Structures to Store Features ---
// v_features[layer_index][atom_id] -> stores vertex feature vector
// e_features[layer_index][edge_tuple] -> stores edge feature vector

// --- Helper Function Placeholders (Conceptual) ---
FUNCTION GetAtomicNumber(atom): RETURN integer
FUNCTION GetInteratomicDistance(pos1, pos2): RETURN float
FUNCTION GetNeighbors(atom, all_atoms, cutoff): RETURN list_of_atoms
FUNCTION CreateEdgeTuple(atom1, atom2): RETURN unique_edge_identifier // e.g., sorted (id1, id2)
FUNCTION CalculateRBFExpansion(distance, num_centers, sigma_rbf): RETURN vector_dim_num_centers
FUNCTION ElementEmbeddingNet(atomic_number): RETURN vector_dim_DIM_V_NODE
FUNCTION MP_VertexUpdateNet_Phi_v(layer_idx, concatenated_z_vector): RETURN vector_dim_DIM_V_NODE
FUNCTION MP_EdgeUpdateNet_Phi_e(layer_idx, concatenated_x_vector): RETURN vector_dim_DIM_E_EDGE_MP
FUNCTION LayerNormalization(vector): RETURN normalized_vector
FUNCTION GetOrientationSphericalHarmonics(center_atom, neighbor_atom, target_edge_for_coord_sys, all_atoms): RETURN vector_dim_DIM_SPHERICAL_HARMONICS
FUNCTION LCMP_VertexUpdateNet_Phi_v(concatenated_y_vector_with_orient): RETURN vector_dim_DIM_V_NODE
FUNCTION LCMP_EdgeUpdateNet_Phi_e(concatenated_x_vector_lcmp, N_orbitals1, N_orbitals2): RETURN vector_dim_(N_orbitals1 * N_orbitals2)
FUNCTION GetNumberOfOrbitals(atomic_number): RETURN integer
FUNCTION ReshapeVectorToMatrix(vector, rows, cols): RETURN matrix
FUNCTION GetRotationMatrix_LocalToGlobal(target_edge_for_coord_sys, all_atoms): RETURN rotation_matrix

// === STEP 0: Initial Feature Embeddings (Layer 0) ===

// v_i^(0): Initial Vertex Features
FOR atom_i IN atoms:
    Z_i = GetAtomicNumber(atom_i)
    v_features[0][atom_i.id] = ElementEmbeddingNet(Z_i)
    // SHAPE: DIM_V_NODE (e.g., 64)
    // MEANING: Learned vector representing the elemental type of atom_i.

// e_ij^(0): Initial Edge Features
FOR edge_ij_tuple IN relevant_edges: // Consists of (atom_i, atom_j)
    atom_i = edge_ij_tuple.atom1
    atom_j = edge_ij_tuple.atom2
    distance_ij = GetInteratomicDistance(atom_i.position, atom_j.position)
    e_features[0][edge_ij_tuple] = CalculateRBFExpansion(distance_ij, NUM_RBF_CENTERS, sigma_rbf_value)
    // SHAPE: DIM_E_EDGE_MP (e.g., 128, as NUM_RBF_CENTERS is 128)
    // MEANING: Feature vector encoding the distance |r_ij| using Gaussian RBFs.

// === STEPS 1 to NUM_MP_LAYERS: Message Passing (MP) Layers ===
// Let current_layer_idx range from 1 to NUM_MP_LAYERS
FOR l_mp FROM 1 TO NUM_MP_LAYERS:
    previous_layer_idx = l_mp - 1

    // --- v_i^(l_mp): Vertex Feature Update ---
    FOR atom_i IN atoms:
        aggregated_messages_for_v_i = NewVector(DIM_V_NODE, fill_with=0.0)
        neighbors_of_i = GetNeighbors(atom_i, atoms, Rc_cutoff)
        FOR neighbor_k IN neighbors_of_i:
            // MAPPING: Concatenate features from previous layer for message input
            v_i_prev = v_features[previous_layer_idx][atom_i.id]         // Shape: DIM_V_NODE
            v_k_prev = v_features[previous_layer_idx][neighbor_k.id]     // Shape: DIM_V_NODE
            edge_ik_tuple = CreateEdgeTuple(atom_i, neighbor_k)
            e_ik_prev = e_features[previous_layer_idx][edge_ik_tuple]    // Shape: DIM_E_EDGE_MP

            concatenated_z_ik = Concatenate(v_i_prev, v_k_prev, e_ik_prev) // Shape: 2*DIM_V_NODE + DIM_E_EDGE_MP (e.g., 64+64+128=256)
            message_from_k_to_i = MP_VertexUpdateNet_Phi_v(l_mp, concatenated_z_ik) // Shape: DIM_V_NODE
            aggregated_messages_for_v_i += message_from_k_to_i

        // Apply update with residual connection and LayerNorm
        v_features[l_mp][atom_i.id] = LayerNormalization(aggregated_messages_for_v_i) + v_features[previous_layer_idx][atom_i.id]
        // SHAPE of v_features[l_mp][atom_i.id]: DIM_V_NODE (e.g., 64)
        // MEANING: Updated embedding for atom_i, incorporating information from its 1-hop neighborhood at the previous layer.

    // --- e_ij^(l_mp): Edge Feature Update ---
    FOR edge_ij_tuple IN relevant_edges:
        atom_i = edge_ij_tuple.atom1
        atom_j = edge_ij_tuple.atom2

        // MAPPING: Concatenate updated vertex features and previous edge feature
        v_i_curr = v_features[l_mp][atom_i.id]         // Shape: DIM_V_NODE (just updated)
        v_j_curr = v_features[l_mp][atom_j.id]         // Shape: DIM_V_NODE (just updated)
        e_ij_prev = e_features[previous_layer_idx][edge_ij_tuple] // Shape: DIM_E_EDGE_MP

        concatenated_x_ij = Concatenate(v_i_curr, v_j_curr, e_ij_prev) // Shape: 2*DIM_V_NODE + DIM_E_EDGE_MP (e.g., 256)
        e_features[l_mp][edge_ij_tuple] = MP_EdgeUpdateNet_Phi_e(l_mp, concatenated_x_ij)
        // SHAPE of e_features[l_mp][edge_ij_tuple]: DIM_E_EDGE_MP (e.g., 128)
        // MEANING: Updated embedding for edge (i,j), reflecting the updated states of atoms i and j.

// === STEP L: Local Coordinate Message Passing (LCMP) Layer ===
// This layer produces the H'_ij representation for each target edge.
// Input features are from layer NUM_MP_LAYERS.
input_layer_idx_for_lcmp = NUM_MP_LAYERS
H_prime_local_vectors = {} // Dictionary to store H'_ij vectors

FOR target_edge_pq IN relevant_edges: // Let the target edge be (atom_p, atom_q)
    atom_p = target_edge_pq.atom1
    atom_q = target_edge_pq.atom2

    // --- 1. Calculate Contextualized Vertex Features for atom_p and atom_q ---
    //    (These are v_p^(LCMP_ctx_pq) and v_q^(LCMP_ctx_pq) used in paper's Eq. 6)

    // For atom_p, in the context of target_edge_pq's local coordinate system:
    aggregated_messages_for_v_p_lcmp = NewVector(DIM_V_NODE, fill_with=0.0)
    neighbors_of_p = GetNeighbors(atom_p, atoms, Rc_cutoff)
    FOR neighbor_k_of_p IN neighbors_of_p:
        v_p_from_mp = v_features[input_layer_idx_for_lcmp][atom_p.id]       // Shape: DIM_V_NODE
        v_k_from_mp = v_features[input_layer_idx_for_lcmp][neighbor_k_of_p.id] // Shape: DIM_V_NODE
        edge_pk_tuple = CreateEdgeTuple(atom_p, neighbor_k_of_p)
        e_pk_from_mp = e_features[input_layer_idx_for_lcmp][edge_pk_tuple]    // Shape: DIM_E_EDGE_MP

        concatenated_z_pk_mp = Concatenate(v_p_from_mp, v_k_from_mp, e_pk_from_mp) // Shape: 256
        orientation_feat_pk_rel_pq = GetOrientationSphericalHarmonics(atom_p, neighbor_k_of_p, target_edge_pq, atoms) // Shape: DIM_SPHERICAL_HARMONICS (25)

        // MAPPING: Concatenate z_pk from MP layer with orientation features
        input_y_for_lcmp_v_update = Concatenate(concatenated_z_pk_mp, orientation_feat_pk_rel_pq) // Shape: 256 + 25 = 281
        message_from_k_to_p_lcmp = LCMP_VertexUpdateNet_Phi_v(input_y_for_lcmp_v_update)     // Shape: DIM_V_NODE
        aggregated_messages_for_v_p_lcmp += message_from_k_to_p_lcmp
    v_p_lcmp_contextual = aggregated_messages_for_v_p_lcmp // This is v_p^(LCMP_ctx_pq)
    // SHAPE: DIM_V_NODE (e.g., 64)
    // MEANING: Feature vector for atom_p, incorporating its neighborhood's orientation relative to target_edge_pq's local coordinate system.

    // Similarly, calculate v_q_lcmp_contextual for atom_q:
    aggregated_messages_for_v_q_lcmp = NewVector(DIM_V_NODE, fill_with=0.0)
    neighbors_of_q = GetNeighbors(atom_q, atoms, Rc_cutoff)
    FOR neighbor_k_of_q IN neighbors_of_q:
        v_q_from_mp = v_features[input_layer_idx_for_lcmp][atom_q.id]
        v_k_from_mp = v_features[input_layer_idx_for_lcmp][neighbor_k_of_q.id]
        edge_qk_tuple = CreateEdgeTuple(atom_q, neighbor_k_of_q)
        e_qk_from_mp = e_features[input_layer_idx_for_lcmp][edge_qk_tuple]

        concatenated_z_qk_mp = Concatenate(v_q_from_mp, v_k_from_mp, e_qk_from_mp)
        orientation_feat_qk_rel_pq = GetOrientationSphericalHarmonics(atom_q, neighbor_k_of_q, target_edge_pq, atoms)
        
        input_y_for_lcmp_v_update_q = Concatenate(concatenated_z_qk_mp, orientation_feat_qk_rel_pq)
        message_from_k_to_q_lcmp = LCMP_VertexUpdateNet_Phi_v(input_y_for_lcmp_v_update_q)
        aggregated_messages_for_v_q_lcmp += message_from_k_to_q_lcmp
    v_q_lcmp_contextual = aggregated_messages_for_v_q_lcmp // This is v_q^(LCMP_ctx_pq)
    // SHAPE: DIM_V_NODE (e.g., 64)
    // MEANING: Feature vector for atom_q, similar to v_p_lcmp_contextual.

    // --- 2. Calculate e_pq^(LCMP) -> H'_pq vector ---
    e_pq_from_mp = e_features[input_layer_idx_for_lcmp][target_edge_pq] // Shape: DIM_E_EDGE_MP (128)

    // MAPPING: Concatenate contextual vertex features and the edge feature from the last MP layer
    input_x_for_lcmp_e_update = Concatenate(v_p_lcmp_contextual, v_q_lcmp_contextual, e_pq_from_mp) // Shape: 64+64+128=256

    N_orbitals_p = GetNumberOfOrbitals(GetAtomicNumber(atom_p))
    N_orbitals_q = GetNumberOfOrbitals(GetAtomicNumber(atom_q))

    H_prime_pq_vector = LCMP_EdgeUpdateNet_Phi_e(input_x_for_lcmp_e_update, N_orbitals_p, N_orbitals_q)
    // SHAPE: N_orbitals_p * N_orbitals_q (e.g., for C-C with 13 orbitals each, 13*13 = 169)
    // MEANING: This vector IS the flattened representation of the Hamiltonian matrix block H'_pq
    //          (between atom_p and atom_q) in the local coordinate system of edge pq.
    H_prime_local_vectors[target_edge_pq] = H_prime_pq_vector

// === STEP L+1: Final Hamiltonian Transformation (Post-GNN) ===
H_global_matrices = {} // Dictionary to store final H_ij matrices

FOR target_edge_pq IN relevant_edges:
    atom_p = target_edge_pq.atom1
    atom_q = target_edge_pq.atom2
    h_prime_pq_flat_vector = H_prime_local_vectors[target_edge_pq]

    N_orbitals_p = GetNumberOfOrbitals(GetAtomicNumber(atom_p))
    N_orbitals_q = GetNumberOfOrbitals(GetAtomicNumber(atom_q))

    // MAPPING 1: Reshape the flat vector to a matrix H'_pq
    H_prime_pq_matrix = ReshapeVectorToMatrix(h_prime_pq_flat_vector, N_orbitals_p, N_orbitals_q)
    // SHAPE: (N_orbitals_p x N_orbitals_q) matrix
    // MEANING: The Hamiltonian block H'_pq in the local coordinate system of edge pq.

    // MAPPING 2: Rotate H'_pq to the global coordinate system to get H_pq
    R_pq_local_to_global = GetRotationMatrix_LocalToGlobal(target_edge_pq, atoms)
    // H_pq = R * H'_pq * R_transpose (if R is orthogonal matrix for coordinate transformation)
    H_pq_global_matrix = R_pq_local_to_global * H_prime_pq_matrix * Transpose(R_pq_local_to_global)
    // SHAPE: (N_orbitals_p x N_orbitals_q) matrix
    // MEANING: The final DFT Hamiltonian matrix block H_pq between atom_p and atom_q
    //          in the global coordinate system.
    H_global_matrices[target_edge_pq] = H_pq_global_matrix

RETURN H_global_matrices
```

## 3. Why covariant? 
### 3.1 To Achieve covariance
**input of DeepH:** 
- $Z_{i}$ of $v_{i}$. 
- $|r_{ij}|$ of $e_{ij}$. 
**output of DeepH**: 
- $H'_{i\alpha,j\beta}$ in a Local Coordinate. 
**then process into:** 
- $H_{i\alpha,j\beta}$ form $H'_{i\alpha,j\beta}$ and a rotation transformation between global basis and local coordinate basis. 

The key idea is to fix all sym possible basis into one single possible basis to train and transform to other global basis. 

### 3.2 To Avoid Discontinuous
deploy **Local Coordinate Massage Passing Layer**.

![[Pasted image 20250513102843.png]]


# Supplementary info

## wigner D matrix in Hamiltonian transfromation. 













