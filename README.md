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

![subplots](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/4700bcf1-35ab-45ff-a798-b3ccfd8ee12f)


Or we canhave the histograms to be shown seperately, each in its own subplot.

```python

# Define a colormap
cmap = cm.get_cmap('viridis', len(df.columns))

# Plotting histograms for each column
for i,column in enumerate(df.columns):
    color = cmap(i)
    plt.figure(figsize=(8, 6))
    plt.hist(df[column], bins=30, color=color, edgecolor='black', density=True, alpha=0.7)
    plt.title(f'Histogram of {column}')
    plt.xlabel('Values')
    plt.ylabel('Probability Density')
    plt.show()
```

![image](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/9453da53-954e-484f-84a0-2207450ff309)

![image](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/3607ca06-8c32-4750-bb53-153fb15a674f)

![image](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/5842733a-da93-4815-8082-475f218da20e)

![image](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/5e6dc4d8-4fa6-41a0-920d-0b570de8965a)


* Boxplots

```python
import matplotlib.pyplot as plt

plt.rcParams.update({"font.family": "Bell MT"})
plt.rcParams.update({'font.size': 14}) 

fig = plt.figure(figsize =(10, 7))
ax = fig.add_subplot(111)
 
# Creating axes instance
bp = ax.boxplot(df, patch_artist = True,
                notch ='True', vert = 0) #notch is the way the plots are narrower in the middle
                                         # vert is the option for showing the boxplots vertically or horizontally
colors = ['#0000FF', '#00FF00', 
          '#FFFF00', '#FF00FF'] #the colors of the plots
 
for patch, color in zip(bp['boxes'], colors):
    patch.set_facecolor(color)
 
# changing color and linewidth of whiskers
for whisker in bp['whiskers']:
    whisker.set(color ='#8B008B',
                linewidth = 1.5,
                linestyle =":")
 
# changing color and linewidth of caps
for cap in bp['caps']:
    cap.set(color ='#8B008B',
            linewidth = 2)
 
# changing color and linewidth of medians
for median in bp['medians']:
    median.set(color ='red',
               linewidth = 3)
 
# changing style of fliers
for flier in bp['fliers']:
    flier.set(marker ='s', 
              color ='#e7298a',
              alpha = 0.5)
     
ax.set_yticklabels(['Normal', 'Exponential', 
                    'Uniform', 'Poisson'])
 
plt.title("Distributions Boxplots")
 
ax.get_xaxis().tick_bottom()
ax.get_yaxis().tick_left()
plt.show()
```

![image](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/d35cdad4-e728-4594-b8ae-0dbd8c0bcb7f)

The source of the above code is [this website](https://www.geeksforgeeks.org/box-plot-in-python-using-matplotlib/).

Moreover, we can show them in different subplots of the same plot:

```python
# Create a figure with subplots
fig, axes = plt.subplots(4, 1, figsize=(10, 14))  # 4 rows, 1 column

# Colors for the boxplots
colors = ['#0000FF', '#00FF00', '#FFFF00', '#FF00FF']

# Plot each distribution in a separate subplot
for ax, (column, color) in zip(axes, zip(df.columns, colors)):
    bp = ax.boxplot(df[column], patch_artist=True, notch=True, vert=0)

    # Set color for boxes
    for patch in bp['boxes']:
        patch.set_facecolor(color)

    # Set color and linewidth for whiskers
    for whisker in bp['whiskers']:
        whisker.set(color='#8B008B', linewidth=1.5, linestyle=":")

    # Set color and linewidth for caps
    for cap in bp['caps']:
        cap.set(color='#8B008B', linewidth=2)

    # Set color and linewidth for medians
    for median in bp['medians']:
        median.set(color='red', linewidth=3)

    # Set style for fliers
    for flier in bp['fliers']:
        flier.set(marker='s', color='#e7298a', alpha=0.5)
    
    # Set title and labels
    ax.set_title(f"{column} Boxplot")
    ax.get_xaxis().tick_bottom()
    ax.get_yaxis().tick_left()
    ax.set_yticklabels([column.split()[0]])

# Set overall title
fig.suptitle("Distributions Boxplots", fontsize=16)

# Adjust layout
plt.tight_layout(rect=[0, 0, 1, 0.96])
plt.show()
```

![image](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/d1b37a8b-7902-4da2-825b-9f2ccd0f9836)

Moreover, boxplots can be generate by seaborn package as well. For more information on the basic of this package please refer to [this link](https://seaborn.pydata.org/generated/seaborn.boxplot.html).

* Violin Boxplots

This kind of plot is used to show both the boxplot and the distribution of a dataset.

```python

# Colors for the violin plots
my_pal = {'limegreen',  'skyblue', 'pink', 'orange'}

ax = sns.violinplot(data=[df['Normal distribution'], df['Exponential distribution'],
                          df['Uniform distribution'], df['Poisson distribution']], 
                    palette=my_pal, inner=None)

#you can apply transparecy to this plot
# for patch in ax.collections:
#     patch.set_alpha(0.3) 

# Adjust violin plot width
for item in ax.collections:
    x0, y0, width, height = item.get_paths()[0].get_extents().bounds
    item.set_clip_path(plt.Rectangle((x0, y0), width/2, height,
                       transform=ax.transData))

# Adjust violin plot offsets
num_items = len(ax.collections)
for item in ax.collections[num_items:]:
    item.set_offsets(item.get_offsets() + 0.15)

# Create boxplot
sns.boxplot(data=[df['Normal distribution'], df['Exponential distribution'],
                          df['Uniform distribution'], df['Poisson distribution']], width=0.25,
            showfliers=True, showmeans=True, 
            meanprops=dict(marker='o', markerfacecolor='maroon',
                           markersize=10, zorder=1),
            boxprops=dict(facecolor=(0,0,0,0), 
                          linewidth=1, zorder=3),
            whiskerprops=dict(linewidth=1),
            capprops=dict(linewidth=1),
            medianprops=dict(linewidth=1))

# Set labels and ticks
ax.set_xticklabels(['Normal\ndistribution', 'Exponential\ndistribution',
                    'Uniform\ndistribution','Poisson\ndistribution'], size=14, fontweight='bold')
ax.set_ylabel("Values", size=16, fontweight='bold')
plt.yticks(fontweight='bold', size=14)
plt.title ('Distributions Violin Boxplots', fontweight='bold')

plt.show()
```

![image](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/3f50f580-8529-4183-8e0b-0736144e992f)


Or show then in different subplots:

```python
# Create a figure with subplots
fig, axes = plt.subplots(2, 2, figsize=(14, 10))  # 2 rows, 2 columns

# Colors for the violin plots
my_pal = ['limegreen', 'skyblue', 'pink', 'orange']

# List of distributions
distributions = ['Normal distribution', 'Exponential distribution', 'Uniform distribution', 'Poisson distribution']

# Plot each distribution in a separate subplot
for ax, column, color in zip(axes.flatten(), distributions, my_pal):
    # Violin plot
    sns.violinplot(ax=ax, data=df[column], color=color, inner=None)
    
    # Adjust violin plot width
    for item in ax.collections:
        x0, y0, width, height = item.get_paths()[0].get_extents().bounds
        item.set_clip_path(plt.Rectangle((x0, y0), width/2, height,
                           transform=ax.transData))

    # Boxplot
    sns.boxplot(ax=ax, data=df[column], width=0.25,
                showfliers=True, showmeans=True, 
                meanprops=dict(marker='o', markerfacecolor='maroon',
                               markersize=10, zorder=1),
                boxprops=dict(facecolor=(0,0,0,0), 
                              linewidth=1, zorder=3),
                whiskerprops=dict(linewidth=1),
                capprops=dict(linewidth=1),
                medianprops=dict(linewidth=1))
    
    # Set labels and ticks
    ax.set_xticklabels([f'{column.split()[0]}\n{column.split()[1]}'], size=14, fontweight='bold')
    ax.set_ylabel("Values", size=16, fontweight='bold')

# Set overall title
fig.suptitle("Distributions Violin Boxplots", fontsize=16, fontweight='bold')

# Adjust layout
plt.tight_layout(rect=[0, 0, 1, 0.96])
plt.show()
```

![image](https://github.com/sadaf-mahmoudi96/Create-Plots/assets/98908606/48550426-d7fe-4374-bf43-f414b366e3ef)












