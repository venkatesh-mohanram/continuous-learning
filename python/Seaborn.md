# Seaborn
Seaborn is a popular plotting/visualizing library and it is on top the matplotlib. 

1. [Distribution Plots](#dist_plots)
2. [Categorical Plots](#catg_plots)
3. [Matrix Plots](#matrix_plots)
4. [Grid Plots](#grid_plots)
5. [Regression Plots](#reg_plots)

``` python
import seaborn as sns
import matplotlib.pyplot as plt
```

<a name="dist_plots"></a>

## Distribution Plots
There are different distribution plots options available based on whether we want to know the distribution for a single variable or two variables

* distplot 
	- for the univarient/single variable distribution
	
* jointplot
	- for two variables, default will be a scatter plot and we can add hue if it contains any categorical columns are there in the data
	 
* pairplot
	- prepares n x n matrix of plots for all the numerical columns available in the dataset. The diagonal will be the univarient plot
	
* rugplot
	- this is for univarient and it adds a dash mark for every point. They are the building blocks of KDE plot (Kernel Density Estimation)
	 
* kdeplot
	- this is also for univarient and shows the Guassian normal distribution 
	
<a name="catg_plots"></a>

## Categorical Plots	

These kinds of plots are for the categirical columns/data like sex, country, continent etc., Seaborn provides lots of different representations for these kind of data

* factorplot
	- it is a general form of plot and accept the kind argument to choose from one of the below plots. eg: kind=box will draw a box plot
* boxplot
	- boxplot shows the distribution of categorical data, it also separate out the outliers. Also additional hue can be added	 
* violinplot
	- similar to boxplot but shows the distribution across several levels such that the distibution can be compared
* stripplot
	- will draw the scaterplot where one data is categorial
* swarmplot
	- similar to stripplot except that it will not overlap the points
* barplot
	- for getting the aggregation of categorical columns, we can pass custom aggregate function like np.std or own own standard deviation function in 'estimator' param
* countplot
	- it counts the number of occurrences of the given categorical column 
	
<a name="matrix_plots"></a>

## Matrix Plots

Used to color encode the values in the Matrix, example are a heatmap which shows the density. For both of these the data should be in a matrix format

* Heatmap
* Clustermap


<a name="grid_plots"></a>

## Grid plots

Grid plots are general type plots that allows to map plot types to rows and column

* PairGrid
	- 	Similar to pairPlot what we seen in distribution plot

``` python
g = sns.PairGrid(iris)
g.map(plt.scatter)

# Map to upper,lower, and diagonal
g = sns.PairGrid(iris)
g.map_diag(plt.hist)
g.map_upper(plt.scatter)
g.map_lower(sns.kdeplot)
```

* Facet Grid
	- To create grid plots based off a feature
	
``` python
g = sns.FacetGrid(tips, col="time",  row="smoker")
g = g.map(plt.hist, "total_bill")
```

* Joint Grid
	- a general version of jointplot where we can set what is the plot type we want to present

``` python
g = sns.JointGrid(x="total_bill", y="tip", data=tips)
g = g.plot(sns.regplot, sns.distplot)
```

<a name="reg_plots"></a>

## Regression plots

* lmplot
	- Used to draw the linear regression model of the given data, x & y. It has additional capability to accept hue, grid etc
	

	