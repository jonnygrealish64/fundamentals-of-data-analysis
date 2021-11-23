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
Streamplots are used to display 2D vector fields and the flow within. 
Streamplots are coded as follows in matplotlib:
ax.streamplot(x_grid, y_grid, x_vec, y_vec, density=spacing)

x_grid and y_grid are arrays of x, y points.
x_vec and y_vec are arrays which denote the velocity of the stream at each point on the grid.
density=spacing establishes how close the space in between streamlines are.

Let's begin with a streamplot that contains stream lines on a 10x10 grid. All the stream lines on this plot are parallel and point horizontally to the right:

import numpy as np
import matplotlib.pyplot as plt
# if using a Jupyter notebook, include:
%matplotlib inline

x = np.arange(0,10)
y = np.arange(0,10)

X, Y = np.meshgrid(x,y)
u = np.ones((10,10)) # x-component to the right
v = np.zeros((10,10)) # y-component zero

fig, ax = plt.subplots()

ax.streamplot(X,Y,u,v, density = 0.5)
ax.set_title('Stream Plot of Parallel Lines')
plt.show()

There are numerous aspects within a streamplot all outlined below:

x, y: these are one-dimensional (1D) arrays, across an evenly spaced grid.

u, v: these are two-dimensional (2D) arrays, x & y-velocities, where the number of rows should match the length of y, the number of columns should match x.

density: this is established as a float or 2-tuple that can control the space in between streamlines. When density = 1, the domain is divided into a 30x30 grid, where density linearly scales the grid. Each cell in the grid can have only one traversing streamline. [density_x, density_y] can be used for various levels of density in both directions.

linewidth: this is established as a numeric or 2D array, this value can vary when a 2D array has the same shape as velocities.

color: this is established as either a matplotlib color code, or a 2D array, to provide color to streamlines in the plot. With a 2D array in the same shape as velocities, the values of color are converted to specific colors via cmap (colormap).

cmap: Colormap, this is used to plot the streamlines and arrows on the plot, which is only ever necessary to implement when using an array input for color.

norm: Normalize, this object is used to scale luminance data to 0, 1. If None, stretch (min, max) to (0, 1). Only necessary when color is an array.

arrowsize: float has the factor in scaling the size of the arrows.

arrowstyle: string, which specifies the style of the arrow where FancyArrowPatch can facilitate.
    
minlength: float, to establish the minimum length of the streamlines in both axes coordinates.

start_points: Nx2 array, the coordinates of starting points for the streamlines. In data coordinates, the same as the x and y arrays.

zorder: int, any number.

Returns:
stream_container: StreamplotSet
    Container object with attributes
        lines: matplotlib.collections.LineCollection of streamlines
        arrows: collection of matplotlib.patches.FancyArrowPatch objects representing arrows half-way along stream lines.

Additional kwargs: hold = [True|False] overrides default hold state.

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
https://problemsolvingwithpython.com/06-Plotting-with-Matplotlib/06.15-Quiver-and-Stream-Plots/
https://www.kite.com/python/docs/matplotlib.pyplot.streamplot
https://www.tutorialspoint.com/matplotlib/matplotlib_pie_chart.htm
https://www.w3schools.com/python/matplotlib_pie_charts.asp
https://www.pythonpool.com/matplotlib-table/
https://towardsdatascience.com/simple-little-tables-with-matplotlib-9780ef5d0bc4