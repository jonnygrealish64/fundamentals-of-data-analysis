# fundamentals-of-data-analysis
Fundamentals of Data Analysis @ GMIT 2021

Assessment (100%)
GitHub Repository (20%):
The repository should contain the following:
10%: A clear and informative README.md, explaining why the repository exists, what’s in it, and how to run the notebooks.
10%: A requirements.txt file that enables someone to quickly run your notebooks with minimal configuration. You should also include any other required files such as data files and image files.

Pyplot Notebook (40%):
Include a Jupyter notebook called pyplot.ipynb that contains the following:
15%: An overview of the matplotlib.pyplot Python package.
25%: An in-depth explanation of three interesting plots from matplotlib.pyplot: streamplot, pie, table:

#1: Streamplot:
Streamplots are used to display 2D vector fields and the flow within, they are coded in matplotlib as follows:
    ax.streamplot(X, Y, u, v, density=spacing)

X & Y are one-dimensional (1D) arrays of x & y axes' ranges, spread across an evenly spaced grid.
x_vec and y_vec (u & v) are two-dimensional (2D) arrays of x & y, known as x & y-velocities, these denote the velocity of the stream at each point on the grid. The number of rows should match the length of y, and the number of columns should match x to ensure an evenly spaced grid.
density=spacing dictates how close the space in between streamlines will be set to, this is established as a float number. When density is given a value of 1, the domain gets divided into a 30x30 grid, where the density scales the grid in a linear fashion.
[density_x, density_y] could also be used for various levels of density that can be set in both directions of flow.
We'll begin with creating a streamplot that contains stream lines on a 10x10 grid, where the stream lines are parallel and point horizontally to the right:

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

x = np.arange(0, 10) # setting range of x-axis
y = np.arange(0, 10) # setting range of y-axis

X, Y = np.meshgrid(x, y) # grid will take in the ranges of x & y
u = np.ones((10, 10)) # x-velocity flows horizontally to the right
v = np.zeros((10, 10)) # y-velocity set to zero, no flow

fig, ax = plt.subplots() # define figure as variable ax with access to subplots

ax.streamplot(X, Y, u, v, density = 0.5)
ax.set_title('Streamplot of Parallel Horizontal Lines')
plt.show()

There are other aspects within a streamplot outlined below:

linewidth: float or 2D array:
    The width of the stream lines. With a 2D array, the line width can be varied across the grid. The array must have the same shape as u & v.

color: matplotlib color code, or 2D array:
    The streamline's color. If given an array, its values are converted to colors via cmap and norm. The array must have the same shape as u & v.

cmap: Colormap:
    Colormap used to plot streamlines and arrows. This is only used if color is an array.

norm: Normalize:
    Normalize object used to scale luminance data to 0, 1. If None, stretch (min, max) to (0, 1). This is only used if color is an array.

arrowsize: float:
    Scaling factor for the arrow size.

arrowstyle: str:
    Arrow style specification. See FancyArrowPatch.

minlength: float:
    Minimum length of streamline in axes coordinates.

start_points: Nx2 array:
    Coordinates of starting points for the streamlines in data coordinates (the same coordinates as the x & y arrays).

zorder: int:
    The zorder of the stream lines and arrows. Artists with lower zorder values are drawn first.

maxlength: float:
    Maximum length of streamline in axes coordinates.

integration_direction: {'forward', 'backward', 'both'}:
    Integrate the streamline in forward, backward or both directions. The default is 'both'.

Returns: stream_container: StreamplotSet
    Container object with attributes:
        lines: LineCollection of streamlines
        arrows: PatchCollection containing FancyArrowPatch objects, representing the arrows half-way along stream lines.

#2: Pie:
Pie charts are used to display a single series of data points, where each value in the series is represented as a wedge (or slice of the pie) with each value shown as a percentage of the entire pie chart.
Matplotlib offers a pie() function that generates a pie chart that represents the data given inside an array.
Each value inside the array represents a slice in the pie chart, where the first slice begins from the x-axis and remaining data moves in an anti-clockwise direction.
The size of each slice is calculated by comparing the slice with the total values, via foodies / sum(foodies)

Each parameter used in constructing a pie chart are outlined below, and all aspects assembled together in the Jupyter notebook, pyplot.ipynb:

foodies:
The foodies array contains numeric values to represent percentages (slices) within the pie chart:
foodies = [12, 10, 45, 8, 25]
ax.pie(foodies, ...)

labels:
The label parameter is used to add string values into another array, to display alongside the numerical values in the pie chart:
foodlabels = ['Curry', 'Burger', 'Pizza', 'Sushi', 'Burrito']
ax.pie(..., labels = foodlabels)

colors:
The color parameter allows the user to specify a color (via hexadecimal values or supported color names) for each slice in the pie chart into an array:
foodcolors = ["Orange", "Yellow", "Red", "Pink", "Brown"]
ax.pie(..., colors = foodcolors)

explode:
The explode parameter is useful for when you want one slice of the pie to stand out from the rest.
The slice in question will extend out from the centre of the pie, via values entered into a separate array:
boom = [0, 0, 0.2, 0, 0]
ax.pie(..., explode = boom)

Starting Point Angle:
The startangle parameter is useful in setting the starting point for data within a pie chart.
The default startangle is set to 0 degrees (3 o'clock), 90 (12 o'clock), 180 (9 o'clock) & 270 (6 o'clock), all values moving in an anti-clockwise direction:
ax.pie(..., startangle = 90)

Auto Percentages:
The auto percentage parameter (autopct) is used to display the numerical values of an array inside their respective wedges as percentage labels inside a pie chart.
The percentages are formatted to each contain one decimal place, 25.0%:
ax.pie(..., autopct = '%1.1f%%')

Shadow:
The shadow parameter adds a shadow effect to the pie chart:
ax.pie(..., shadow = True)

Legend:
The legend parameter is used to display a list, in order to explain each slice and their respective titles and colors within the pie chart, along with adding a title to the legend:
plt.legend(title = "Five Popular Fast Foods :P")

#3: Table:
The table() function is used in Python to create tables or add a table to axes.
The important parameters within the table() function are outlined below:
matplotlib.pyplot.table(
    cellText = 2D list with string values: this is the text to be placed within the cells of the table,
    cellColours = 2D list of matplotlib color specs: this sets the background colours of cells,
    cellLoc = {'left', 'center', 'right'}: this aligns the values within cells, 'right' is set as the default,
    colWidths = list of float: this sets the width of the columns,
    rowLabels = list of strings: this contains the text of the cells of the rows,
    rowColours = list of matplotlib color specs: this sets the row colours in the table,
    rowLoc = {'left', 'center', 'right'}: this aligns the values within rows, 'left' is set as the default,
    colLabels = list of strings: this contains the text of the cells of the columns,
    colColours = list of matplotlib color specs: this sets the column colours in the table,
    colLoc = {'left', 'center', 'right'}: this aligns the values within columns, 'center' is set as the default,
    loc = string: this is the position of the cell with respect to the axes, 'bottom' is set as the default,
    bbox = Bbox: this is a bounding box to insert the table into,
    edges = {'open', 'closed', 'horizontal', 'vertical'}: the cell edges to be drawn with a line, 'closed' is set as the default,
    **kwargs
                       )

One method of creating a table is via the use of custom values entered by the user:
    the table_data array is passed into the cellText parameter as follows: (cellText = table_data),
    the column names can be specified with the colLabels parameter: (colLabels = column_labels)
    the table is placed at the center of the respective axes via: (loc = "center")

import matplotlib.pyplot as plt
fig, ax = plt.subplots(1, 1)
table_data = [
              [10, 24, 37],
              [55, 69, 76],
              [84, 96, 108]
             ]
column_labels = ["Column 1", "Column 2", "Column 3"]
ax.axis('tight')
ax.axis('off')
ax.table(
         cellText = table_data,
         colLabels = column_labels,
         loc = "center"
        )

A second method we can use to generate a table is passing a Pandas DataFrame and a NumPy array as a cellText parameter.
This generates the table via the Pandas DataFrame, df.
The values of df are passed into the cellText parameter, and the column names of df are passed into the colLabels parameter, and the rowLabels parameter acts as a label for the rows in the table:

import pandas as pd
import matplotlib.pyplot as plt
fig, ax = plt.subplots(1, 1)
table_data = [
              [10, 24, 37],
              [55, 69, 76],
              [84, 96, 108]
             ]
column_labels = ["Column 1", "Column 2", "Column 3"]
df = pd.DataFrame(data, columns = column_labels)
ax.axis('tight')
ax.axis('off')
ax.table(
         cellText = df.values,
         colLabels = df.columns,
         rowLabels = ["A", "B", "C"],
         loc = "center"
        )
plt.show()

We can also add colours to particular fields in order to distinguish the row and column labels, using the rowColours and colColours parameters:
ax.table(
         cellText = df.values,
         colLabels = df.columns,
         rowLabels = ["Row A", "Row B", "Row C"],
         rowColours = ["orange"] * 3,
         colColours = ["green"] * 3,
         cellLoc = "center",
         loc = "center"
        )
We can also modify the created table by passing in parameters (**kwargs) to modify font size of data points, or scaling the entire table to a specified size, etc:
table.set_fontsize(15)
table.scale(1, 3)

CAO Points Notebook (40%):
Include a Jupyter notebook called cao.ipynb that contains the following:
10%: An overview of how to load CAO points info from the CAO website into a pandas data frame.
20%: A detailed comparison of CAO points in 2019, 2020, and 2021 using pandas functionality.
10%: Appropriate plots and other visualisations to enhance your notebook for viewers.

References:
https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.html
https://www.w3schools.com/python/matplotlib_pyplot.asp
https://towardsdatascience.com/a-practical-summary-of-matplotlib-in-13-python-snippets-4d07f0011bdf
https://matplotlib.org/3.1.1/gallery/images_contours_and_fields/plot_streamplot.html#sphx-glr-gallery-images-contours-and-fields-plot-streamplot-py
https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.streamplot.html
https://problemsolvingwithpython.com/06-Plotting-with-Matplotlib/06.15-Quiver-and-Stream-Plots/
https://www.tutorialspoint.com/matplotlib/matplotlib_pie_chart.htm
https://www.w3schools.com/python/matplotlib_pie_charts.asp
https://www.pythonpool.com/matplotlib-table/
https://www.delftstack.com/howto/matplotlib/plot-table-using-matplotlib/
https://docs.w3cub.com/matplotlib~3.1/_as_gen/matplotlib.pyplot.table
https://www.statology.org/matplotlib-table/