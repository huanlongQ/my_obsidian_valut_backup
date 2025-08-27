-  [itertools — Functions creating iterators for efficient looping — Python 3.13.7 documentation](https://docs.python.org/3/library/itertools.html)

阅. 

**Here, itertools.product gives** `(0,0),(0,1),(1,0),(1,1)` **pairs.** 
```python
import numpy as np
from itertools import product
def block_spin_rg(spins: np.ndarray) -> np.ndarray:
    """
    Perform one 2×2×... block-spin RG step on an ND Ising configuration.

    Args:
        spins (np.ndarray): integer array of shape (L, L, ..., L), L even,
                            entries must be +1 or -1.

    Returns:
        np.ndarray: blocked spins of shape (L//2, L//2, ..., L//2), entries +1 or -1.
    """
    # check shape
    if any(sz % 2 != 0 for sz in spins.shape):
        raise ValueError("Each dimension must be even-sized for 2×2 blocking.")

    d = spins.ndim
    # sum over all 2^d offsets
    # e.g. for d=2: offsets = (0,0),(0,1),(1,0),(1,1)
    sum_spins = None
    for bits in product((0,1), repeat=d):
        # construct slicing tuple like (slice(bit, None, 2),)*d
        sl = tuple(slice(b, None, 2) for b in bits)
        # **here, slice(start, end, steps) makes good slice for spins.** 
        block = spins[sl]
        # **this is the vote procedure.**
        if sum_spins is None:
            sum_spins = block.astype(block.dtype).copy()
        else:
            sum_spins += block

    # now sum_spins has shape (L//2, L//2, ..., L//2), values in {-2^d, ..., +2^d}
    # majority rule: positive sum → +1, negative → -1, zero → random choice
    rged = np.where(sum_spins > 0, 1, -1)

    # handle ties (sum == 0)
    ties = (sum_spins == 0)
    if np.any(ties):
        # generate random ±1 for each tie
        # note: you can set np.random.seed(...) externally for reproducibility
        rand_choices = np.random.choice([-1, 1], size=ties.sum())
        rged[ties] = rand_choices

    return rged
```
