---
layout: post
title: Plotting in Python
date: 2020-02-10 17:03:00 --0000
permalink: /posts/python-plotting/
---

## Matplotlib

### Bar charts
Official documentation: [here](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html)

Example:
```python
plt.rcdefaults()
fig, ax = plt.subplots(figsize=(8, 6))
ax.barh(states, amount) # if horizontal bar
ax.invert_yaxis() # labels read top-to-bottom
plt.show();
```

## Seaborn

Sometimes we have multiple groups in the data and we would like to generate a plot for each of the groups. First we import the data set:
```
psg = pd.read_stata('dta_files/perc_suicide_gun.dta')
```
And then we can plot using the seaborn package
```
g = sns.FacetGrid(psg, col="statename", col_wrap=3, height=4)
g = (g.map(plt.scatter, "year", "perc_gun", edgecolor="w").add_legend()) # "year" would be on the x axis and "perc_gun" would be on the y axis
for ax in g.axes.flat:
    ax.set_ylim([0,1])  # set the range for the y axis
    ax.xaxis.set_major_locator(plt.AutoLocator())
    _ = plt.setp(ax.get_xticklabels(), visible=True) # in order to keep track of which group we are referring to
    _ = plt.setp(ax.get_yticklabels(), visible=True)
plt.show() # show the figure inline
g.savefig("perc_suicide_gun.jpg") # save the results as a figure
```
Part of the results are as below:

![Plotting](/images/plotting.jpg "Plotting by the Group")
