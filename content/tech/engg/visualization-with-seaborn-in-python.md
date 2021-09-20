---
title: "Visualization with Seaborn in Python"
date: 2021-07-09T23:48:29+05:30
draft: false
katex: fasle
tags: ["Data Science", "Visualization"]
categories: ["🗃️ Tech", "🧰 Engg"]
typora-root-url: ../../../static
---

Seaborn is a high level visualisation tool built on top of matplotlib which enables us to work with dataframes easily. We will try to make use of [this Automobile dataset]( /files/2021/visualization-with-seaborn-in-python/Automotive.csv) and try to gain some information with the help of seaborn plots. This post will be an exploratory one.


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
```



The following plots are made similar to [this post](https://www.analyticsvidhya.com/blog/2019/09/comprehensive-data-visualization-guide-seaborn-python/) but with a different dataset.

The plotting will be divided into two sections,

1. Visualizing statistical relationships
2. Plotting categorical data

Let's find import the dataset

```python
autodf = pd.read_csv("Automobile.csv")
autodf.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>symboling</th>
      <th>normalized_losses</th>
      <th>make</th>
      <th>fuel_type</th>
      <th>aspiration</th>
      <th>number_of_doors</th>
      <th>body_style</th>
      <th>drive_wheels</th>
      <th>engine_location</th>
      <th>wheel_base</th>
      <th>...</th>
      <th>engine_size</th>
      <th>fuel_system</th>
      <th>bore</th>
      <th>stroke</th>
      <th>compression_ratio</th>
      <th>horsepower</th>
      <th>peak_rpm</th>
      <th>city_mpg</th>
      <th>highway_mpg</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>168</td>
      <td>alfa-romero</td>
      <td>gas</td>
      <td>std</td>
      <td>two</td>
      <td>convertible</td>
      <td>rwd</td>
      <td>front</td>
      <td>88.6</td>
      <td>...</td>
      <td>130</td>
      <td>mpfi</td>
      <td>3.47</td>
      <td>2.68</td>
      <td>9.0</td>
      <td>111</td>
      <td>5000</td>
      <td>21</td>
      <td>27</td>
      <td>13495</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>168</td>
      <td>alfa-romero</td>
      <td>gas</td>
      <td>std</td>
      <td>two</td>
      <td>convertible</td>
      <td>rwd</td>
      <td>front</td>
      <td>88.6</td>
      <td>...</td>
      <td>130</td>
      <td>mpfi</td>
      <td>3.47</td>
      <td>2.68</td>
      <td>9.0</td>
      <td>111</td>
      <td>5000</td>
      <td>21</td>
      <td>27</td>
      <td>16500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>168</td>
      <td>alfa-romero</td>
      <td>gas</td>
      <td>std</td>
      <td>two</td>
      <td>hatchback</td>
      <td>rwd</td>
      <td>front</td>
      <td>94.5</td>
      <td>...</td>
      <td>152</td>
      <td>mpfi</td>
      <td>2.68</td>
      <td>3.47</td>
      <td>9.0</td>
      <td>154</td>
      <td>5000</td>
      <td>19</td>
      <td>26</td>
      <td>16500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>164</td>
      <td>audi</td>
      <td>gas</td>
      <td>std</td>
      <td>four</td>
      <td>sedan</td>
      <td>fwd</td>
      <td>front</td>
      <td>99.8</td>
      <td>...</td>
      <td>109</td>
      <td>mpfi</td>
      <td>3.19</td>
      <td>3.40</td>
      <td>10.0</td>
      <td>102</td>
      <td>5500</td>
      <td>24</td>
      <td>30</td>
      <td>13950</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>164</td>
      <td>audi</td>
      <td>gas</td>
      <td>std</td>
      <td>four</td>
      <td>sedan</td>
      <td>4wd</td>
      <td>front</td>
      <td>99.4</td>
      <td>...</td>
      <td>136</td>
      <td>mpfi</td>
      <td>3.19</td>
      <td>3.40</td>
      <td>8.0</td>
      <td>115</td>
      <td>5500</td>
      <td>18</td>
      <td>22</td>
      <td>17450</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 26 columns</p>
</div>

It can be observed that the dataset has almost equal share of categorical and numerical dataset. We can check that as,

```python
autodf.dtypes
```

```
symboling                int64
normalized_losses        int64
make                    object
fuel_type               object
aspiration              object
number_of_doors         object
body_style              object
drive_wheels            object
engine_location         object
wheel_base             float64
length                 float64
width                  float64
height                 float64
curb_weight              int64
engine_type             object
number_of_cylinders     object
engine_size              int64
fuel_system             object
bore                   float64
stroke                 float64
compression_ratio      float64
horsepower               int64
peak_rpm                 int64
city_mpg                 int64
highway_mpg              int64
price                    int64
dtype: object
```

With the above information as the basis, let's start exploring the relationships within data.

## Visualizing statistical relationships

Statistical relationships are drawn between numerical data with the aim of understanding how one variable affects other, if at all.

Scatter plot is drawn using `relplot()` function of seaborn. Let's start with the obvious ones, checking whether the horsepower and price are related.

```python
sns.relplot(x="horsepower", y="price", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1ded91a5370>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure4_1.png)

Based on the above plot, one can expect a positive correlation between the horsepower and price. But, can there be any other factor that affect the price, say the make?

```python
sns.relplot(x="horsepower", y="price", hue="make", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1ded91a5400>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure5_1.png)

or the body style?

```python
sns.relplot(x="horsepower", y="price", hue="body_style", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbb75b50>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure6_1.png)

So far, we have given the categorical data for the hue parameter. But, numerical data can also be used.

```python
sns.relplot(x="horsepower", y="price", hue="highway_mpg", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbd2f550>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure7_1.png)

The cheaper ones seem to churn out higher mpg than the counterpart. We can also check that with the help of `size` parameter.

```python
sns.relplot(x="horsepower", y="price", size="city_mpg", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbb9bdc0>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure8_1.png)

## Visualizing categorical data

In order to visualize the categorical data, we will use the `catplot()` function from the seaborn library.

#### Jitter Plot

Initially, we will draw the relationship between the body style(categorical data) and curb weight(numerical data).

```python
sns.catplot(x="body_style", y="curb_weight", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbdc7d60>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure9_1.png)

The above plot is, similar to the title, jittered. They can be lined up by changing the `jitter` parameter.

```python
sns.catplot(x="fuel_system", y="peak_rpm", jitter = False, data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbf00370>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure10_1.png)

#### Hue Plot

Similar to the `relplot()`, we can add another dimension to the picture with the `hue` parameter.

```python
sns.catplot(x="body_style", y="curb_weight", hue="fuel_system", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbde0d90>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure11_1.png)

#### Swarm Plot

The above plot has overlaps which can be eliminated by setting the parameter `kind` to `swarm`. This uses an algorithm which organizes the points intelligently and eliminates the overlap.

```python
sns.catplot(x="body_style", y="curb_weight", hue="fuel_system", kind="swarm", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbe9caf0>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure12_1.png)

#### Box Plot

Box plot shows the quartile values, extremas and the outliers for each category with respect to some numerical relation. This is obtained by setting the `kind` parameter to `box`.

```python
sns.catplot(x="body_style", y="price", kind= "box", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbcce400>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure13_1.png)

We can also include the hue parameter to it.

```python
sns.catplot(x="body_style", y="price", hue="drive_wheels", kind="box", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedc839b20>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure14_1.png)

#### Violin Plot

Violin plot is a richer version of the boxplot as it includes the aforementioned data and enriches it with the kernel density information.

```python
sns.catplot(x="body_style", y="price", kind= "violin", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedd22c5b0>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure15_1.png)

In addition to that, if the hue is added for a binary categorical data and enable the `split` parameter, we get the plot as follows:

```python
sns.catplot(x="body_style", y="price", hue="number_of_doors", kind= "violin", split=True, data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbe6aac0>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure16_1.png)

#### Bar Plot

```python
sns.catplot(x="body_style", y="price", hue="number_of_doors", kind= "bar", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedc7a63a0>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure17_1.png)

#### Point Plot

Point plot shows the estimated value and confidence interval for each hue. The vertical line shows the confidence interval for each category.

```python
sns.catplot(x="body_style", y="curb_weight", hue="fuel_system", kind="point", data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbb8bbe0>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure18_1.png)


## Visualizing Distribution of dataset

### Plotting Univariate Distribution

#### Histograms

In seaborn, the `displot()` function plots the histogram fro the specified series in the dataset. By default, it hides the kernel density estimate for the data which can be turned on by setting the parameter `kde` to `True`. The function `histplot()` has the similar functionality.

```python
sns.displot(autodf.price, kde=True)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedfe1f5b0>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure19_1.png)

#### Rug plot

Another representation will be the rugplot which draws a stick at every observation.

```python
sns.displot(autodf.price, rug=True)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedbd3f280>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure20_1.png)

### Plotting Bivariate Distribution

Bivariate distributions show how two variables vary with respect to each other. This can be plotted using the `jointplot()` function.

```python
sns.jointplot(x="horsepower", y="city_mpg", data=autodf)
```

```
<seaborn.axisgrid.JointGrid at 0x1dedfe28b80>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure21_1.png)

There's a clear negative correlation between the two as one may expect.

#### Hex Plot

Hex plot is another way to visualize where the data are put in hexagonal bins for each pair of the bars on the edges.

```python
sns.jointplot(x="horsepower", y="city_mpg", kind="hex", data=autodf)
```

```
<seaborn.axisgrid.JointGrid at 0x1dedf354b50>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure22_1.png)

#### KDE Plot

This can be plotted by setting the `kind` to `kde`.

```python
sns.jointplot(x="horsepower", y="city_mpg", kind="kde", data=autodf)
```

```
<seaborn.axisgrid.JointGrid at 0x1dedf44f640>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure23_1.png)


#### Heatmaps

Heatmaps can be used to get the general correlation between the variables.

```python
corrmat = autodf.corr()
sns.heatmap(corrmat, vmax=.8, square=True)
```

```
<AxesSubplot:>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure24_1.png)


#### Boxen Plots

Boxen plots are similar to box plots but can also be used to infer the bivariate relations as gives insight for the shape of the distributions.

```python
sns.catplot(x="peak_rpm", y="city_mpg", hue="number_of_doors", kind="boxen", height=4, aspect=3, data=autodf)
```

```
<seaborn.axisgrid.FacetGrid at 0x1dedd215790>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure25_1.png)

### Visualizing Pairwise Relationships

Finally, we take a look at generating the pairwise plot between all the variables in the dataset. This is achieved with the help of the `pairplot()` function. This also plots the univariate data along the diagonal of the plot which can be replaced with the KDE by passing the corresponding value to `diag_kind` parameter.

```python
sns.pairplot(autodf, diag_kind="kde")
```

```
<seaborn.axisgrid.PairGrid at 0x1dedc75b4c0>
```

![](/images/2021/visualization-with-seaborn-in-python/visualisation-with-seaborn_figure26_1.png)

The above plots have given me a good introduction to the seaborn library. I indent to proceed further with visualizing and exploring data with python and the related libraries for a while and seaborn seems to provide the same kind of easiness as Julia plots. This feels like a good starting point!
