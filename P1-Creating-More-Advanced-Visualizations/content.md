---
title: "Diving Into the Pokemon Dataset"
slug: poke-dataset
---

Part 4: Exploratory Data Science (STRETCH CHALLENGE)

# Pokemon Dataset

Let's move on to new, more exciting datasets - data surrounded in pop culture and a captivation to any 90's kids out there!

That's right, it's time to play with **Pokémon**!

For this tutorial, we'll mainly be using Seaborn to develop some advanced visualizations.

We'll follow the same process of question-driven data analysis and processing, but with a significant step up for this particular dataset: we'll assume that our data is *already cleaned and processed*.

Let's take a look at our data!

You can access the [Pokémon (First-Generation)](https://elitedatascience.com/wp-content/uploads/2017/04/Pokemon.csv) dataset here! No need to download or set anything up; if you followed the setup instructions correctly, you should have the dataset already downloaded in your local directory!

Let's jump right in!

# New Jupyter Notebook

Open up a new Jupyter Notebook and title it something like `pokemon_EDA.ipynb`.

In our first cell, let's immediately run our basic setup.

```py
import pandas as pd
import matplotlib.pyplot as plt
% matplotlib inline
import seaborn as sns
```

(Make sure you run the cell before doing anything else - without running the cell, our notebook won't recognize any commands using Pandas, MatPlotLib, or Seaborn!)

Now, let's take a look at our data!

Run the following in a new cell:

```py
df = pd.read_csv('datasets/pokemon.csv', index_col=0)
df.head()
```

> NOTE:

As you may recall. the `.head()` function in Pandas allows us to peek at the first five rows in any dataset. Handy, huh?

Let's take a look at the descriptive statistics for our data as a whole so we can get a better understanding as to effective questions to ask.

```py
df.describe()
```

> NOTE: Add .describe() results here.

We can see that we're dealing with mainly numerical integer data through all our Pokémon statistics. Good! No red flags here.

---

As any basic Pokémon enthusiast understands, two of the most critical stats to look for in any Pokémon are our *Attack* and *Defense* stats, also dubbed **ATK** and **DEF**.

Let's create a basic Seaborn scatterplot to take a look into the distribution of ATK-DEF stats across our Pokémon!

```py
sns.lmplot(x="ATK", y="DEF", data=df)
```

> NOTE: Show scatterplot results.
> NOTE: Talk about `.lmplot()` as a regression line function

```py
# Improved Scatterplot Tutorial
sns.lmplot(x="ATK", y="DEF", data=df, fit_reg=False, hue='Stage')

# MatPlotLib Customization
plt.ylim(0, None)
plt.xlim(0, None)

# Creating a Cool Box Plot
stats_df = df.drop(["Total", "Stage", "Legendary"], axis=1)
sns.boxplot(data=stats_df)

# Creating a Neat Violin Plot
sns.set_style("whitegrid")
sns.violinplot(x="Type 1", y="ATK", data=df)

# Tuning our color palette for the data
pokemon_palette = ['#78C850',  # Grass
                    '#F08030',  # Fire
                    '#6890F0',  # Water
                    '#A8B820',  # Bug
                    '#A8A878',  # Normal
                    '#A040A0',  # Poison
                    '#F8D030',  # Electric
                    '#E0C068',  # Ground
                    '#EE99AC',  # Fairy
                    '#C03028',  # Fighting
                    '#F85888',  # Psychic
                    '#B8A038',  # Rock
                    '#705898',  # Ghost
                    '#98D8D8',  # Ice
                    '#7038F8',  # Dragon
                   ]
sns.violinplot(x="Type 1", y="ATK", data=df, palette=pokemon_palette)

# Creating a Swarm Plot
sns.swarmplot(x="Type 1", y="ATK", data=df, palette=pokemon_palette)

# Creating an Overlayed Violin-Swarm Plot
plt.figure(figsize=(10,6))
sns.violinplot(x="Type 1",
               y="ATK",
               data=df,
               inner=None,
               palette=pokemon_palette)
sns.swarmplot(x="Type 1",
              y="ATK",
              data=df,
              color='k',
              alpha=0.7)
plt.title("Attack by Type")

# Creating a correlation heatmap of stats
corr = stats_df.corr()
sns.heatmap(corr)

# Creating a histogram
sns.distplot(df.Attack)

# Creating a Bar Plot
sns.countplot(x="Type 1", data=df, palette=pokemon_palette)
plt.xticks(rotation=-45)

# Creating a Factor Plot
viz = sns.factorplot(x="Type 1",
                   y="ATK",
                   data=df,
                   hue="Stage",
                   col="Stage",
                   kind="swarm")
viz.set_xticklabels(rotation=-45)

# Creating a Density Plot
sns.kdeplot(df.Attack, df.Defense)

# Creating a Joint Distribution Plot
sns.jointplot(x="ATK", y="DEF", data=df)

# Creating a Kickass Pair Plot
sns.pairplot(iris)

> NOTE: Add more Seaborn tutorials here!
```

[link to pair plot](https://seaborn.pydata.org/generated/seaborn.pairplot.html)
