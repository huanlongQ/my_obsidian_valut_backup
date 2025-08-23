- [tenpy tutorial](https://tenpy.readthedocs.io/en/latest/intro/model.html#what-is-a-model)
- [zhihu tenpy tutorial](https://zhuanlan.zhihu.com/p/714201120) this website gives a brief tutorial.
	this tutorial is much better than tenpy's official documentation.  
	[沪上风老师的GitHub集成QuantumPackage, 自用Python集成程序](https://github.com/Moke2001/QuantumPackage?tab=readme-ov-file)  
![[Pasted image 20250330123755.png|859]] 

# 1. Simulations

# 2. Models

## 2.1 Site as Local Hilbert Space Basis

The **local Hilbert** space is represented by a [`Site`](https://tenpy.readthedocs.io/en/latest/reference/tenpy.networks.site.Site.html#tenpy.networks.site.Site "tenpy.networks.site.Site") (read its doc-string!). A site defines the meaning of each basis state (i.e. by fixing an order, to define e.g. that the state are `spin_down, spin_up`). **Additionally, it stores common local operators, such as Sz and makes them accessible by name.**  
Tenpy `site.py` has Site or Inheritance Site class: `Site, SpinHalfSite, SpinSite, FermionSite, SpinHalfFermionSite, BosonSite` 
**parameters of `Site`:**
- `conserve` or `cons_N` or `cons_Sz`etc: as a RuleBook, tell the model Hamiltonian that some `str` observation is a conserved quantity. 
- `sort_charge`: to determine whether do sort to quantum numbers when establish a `Site` obj.
- `filling` and `Nmax`: for Bosonic syy, `filling` for avg particle number while `Nmax` for max permitted particle number on a specific site. 
- `chinfo: ChargeInfo`: ChargeInfo obj is rulebook for the entire simulation. 
	`chinfo = npc.ChargeInfo([1], ['2 * Sz'])` is a typical code line. 
	`[1]` for adding type: `1` for standard interger addition while `2` for standard addition modulo 2(parity conservation: like fermions can only create and annihilate in pairs)  
	typical charges like `N, Sz, N%2, k` etc. 
	
- `leg: LegCharge`: **physical legs** of MPS
	constructed by 
	`leg:LegCharge = npc.LegCharge(chinfo, slice: Array as slice like[::], charge: 2D Array 2D for different charges)`
	`leg:LegCharge = npc.LegCharge.from_qflat(chargeinfo = chinfo, qflat = [1, -1, 1])` 
	![[Pasted image 20250623220139.png]]
**methods of `Site`:**
- `add_op(name:str, op:npcArray)`: add a op to some site
- `remove_op(name:str)`: remove a op
- `get_op(name)-> npcArray`: .
**attr of `Site`:** 
- `opnames`: get all `op`'s name. 
**essence of `Site`:`npc.Array`**
- `npc.Array = np.NDArray + labels for each axis + npc.LegChrage(from ChargeInfo)`

## 2.1 MPO as a Big Bang: Very Hard.

people choose **finite states machine** to generate normal MPOs:
- [有限状态自动机生产MPO](https://zhuanlan.zhihu.com/p/382361509) 
- [自动生成MPO的算法实现](https://zhuanlan.zhihu.com/p/385274056) 
![[Pasted image 20250626150000.png]] 
![[Pasted image 20250626150432.png]] 
each virtual leg dim means a finite state machine state. 
![[Pasted image 20250626151001.png]] 
we have module `MPO` for Model Construction. 
**Construction:** `some_mpo:MPO = MPO(sites:list[Site], Ws: list[npc.Array], bc:str, IdL:int, IdR:int, etc)`
**attr:**
- `_W`: `list[npc.Array]`, in which `npc.Array includes labels = ['wL', 'wR', 'p', 'p*'], legcharges = list[LegCharge].`
- `dim`: means `shape`
- `L`: length of model
- `chi`: `wL,wR` of each `W`

# 3. Details on the Implementation of Models

# 4. Details on the Lattice Geometry

# 5. Saving to Disk

# 6. Logging and Terminal Output

# 7. Parameters and Options

# 8. Measurements for Simulations

# 9. Charge Conservation with np_conserved
