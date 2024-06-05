This repository contains code about creating interesting plots in Python.

1. Loading the data

First we need to load\create the data:

```python 
import pandas as pd

import numpy as np

np.random.seed(0)  # For reproducibility

data = {
    'A': np.random.normal(loc=50, scale=10, size=100),  # Normal distribution
    'B': np.random.exponential(scale=1, size=100),      # Exponential distribution
    'C': np.random.uniform(low=20, high=80, size=100),  # Uniform distribution
    'D': np.random.poisson(lam=3, size=100)             # Poisson distribution
}

# Creating a dataframe
df = pd.DataFrame(data)
```

2. Creating the plots

Next, we create the plots:

*Histogram


