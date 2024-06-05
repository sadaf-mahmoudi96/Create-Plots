This repository contains code about creating interesting plots in Python.

1. Loading the data

First we need to load\create the data:

```python 
import pandas as pd
import numpy as np

np.random.seed(0)  # For reproducibility

data = {
    'Normal distribution': np.random.normal(loc=50, scale=10, size=100), 
    'Exponential distribution': np.random.exponential(scale=1, size=100),     
    'Uniform distribution': np.random.uniform(low=20, high=80, size=100), 
    'Poisson distribution': np.random.poisson(lam=3, size=100)            
}

# Creating a dataframe
df = pd.DataFrame(data)
```

2. Creating the plots

Next, we create the plots:

* Histogram

The plots can be overlapping:

```python
import matplotlib.pyplot as plt

plt.rcParams.update({"font.family": "Bell MT"}) #you can specify the font of the texts on the plots
plt.rcParams.update({'font.size': 14}) #you can specify the font size of the texts on the plots, Python will use this font all over the code, unless said otherwise.

plt.hist(df['Normal distribution'], bins=30, color='limegreen', edgecolor='black', density=True, label='Normal Distribution', alpha=0.7) #alpha is the transparency
plt.hist(df['Exponential distribution' ], bins=30, color='skyblue', edgecolor='black', density=True, label='Exponential Distribution', alpha=0.6)
plt.hist(df['Uniform distribution'], bins=30, color='pink', edgecolor='black', density=True, label='Uniform Distribution', alpha=0.5)
plt.hist(df['Poisson distribution' ], bins=30, color='orange', edgecolor='black', density=True, label='Poisson Distribution', alpha=0.6)
plt.legend()
plt.xlabel('Values')
plt.ylabel('Probability Density')
plt.title('Histogram of Different Distributions')
#plt.savefig('*.png', dpi=300) #you can also save your plot
plt.show()
```

‎![Alt text](https://github.com/sadaf-mahmoudi96/Create-Plots/tree/main/Histograms/Overlay_Histograms.png)‎‎

You can find the lists of colors in python [here](https://matplotlib.org/stable/gallery/color/named_colors.html).




