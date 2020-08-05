# Matplotlib
Popular library for plotting in Python

In python code, we need to import it like
```shell script
import matplotlib.pypolt as plt
```

## Basic plotting
Matplotlib supports plotting using a basic as well as Object Oriented way of plotting the charts

```shell script
plt.plot(X, Y)  # Where X and Y are py array or a NumPyArray of same size
plt.plot(X, Y, 'r') # Plot the graph in red color
plt.xlabel('X Axis title')
plt.ylabel('Y Axis title')
plt.title('Graph title')
plt.show()
```
## Multiplot
Multi plot means having a set of graphs in the same plot canvas, Matplotlib can divide the canvas into rows and columns. Each plot is called as subplot
```shell script
plt.subplot(nrows, ncols, plot_number)   # number of rows, number of columns, the current plot number
plt.plot(x, y)
```

## Object Oriented plotting
Matplotlib supports object oriented way of creating the plots
```shell script
figure = plt.figure()
figure = plt.figure(figsize=(8, 4), dpi=100)   # Create a figure using the figure size and the dpi
# Each subplot is called as axes
axes1 = figure.add_axes(0.1, 0.1, 0.9, 0.8)  # left, bottom, width, height with the canvas area
axes1.plot(x,y)
```
We can use subplots() similar to basic multiplot but here it returns a figure and axes array
```shell script
fig, axes = plt.subplots(2, 3)  # 2 x 3 = 6 axes in one figure
```
We can save the figures as a image file
```shell script
fig.savefig("file_plot.png")
```
Setting the legends
```shell script
axes1.legend(loc=0)  # 0 - optimal, 1 - upper right, 2 - upper left, 3 - lower right, 4 - lower left
```
  