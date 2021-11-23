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
https://towardsdatascience.com/simple-little-tables-with-matplotlib-9780ef5d0bc4