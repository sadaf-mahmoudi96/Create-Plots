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

The plots can be overlaying:

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
![Overlay Histograms](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/43da20e2-5d5d-417e-92fb-921f85ede930)‎‎

You can find the lists of colors in python [here](https://matplotlib.org/stable/gallery/color/named_colors.html).

The histograms can be shown in the form of subplots in a plot:

```python
import matplotlib.cm as cm

# Plotting histograms in the form og subplots
fig, axes = plt.subplots(nrows=2, ncols=2, figsize=(12, 10))

# Column names
columns = df.columns

# Define a colormap to show each subplot with a distinct color
cmap = cm.get_cmap('viridis', len(df.columns))

# Plotting each histogram in a subplot
for i, ax in enumerate(axes.flatten()):
    color = cmap(i)  # Get a distinct color from the colormap
    ax.hist(df[columns[i]], bins=30, color=color, edgecolor='black', density=True, alpha=0.7)
    ax.set_title(f'Histogram of {columns[i]}')
    ax.set_xlabel('Values')
    ax.set_ylabel('Probability Density')

# Adjust layout
plt.tight_layout()

# Display the plot
plt.show()
```

![subplots](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/f1c529e1-272e-4db5-9b31-f3bade331c69)




