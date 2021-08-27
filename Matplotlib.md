### Interface

    fig, ax = plt.subplots()
    fig, ax = plt.subplots(num-rows, num-cols) 
this allows us to create two objects Figure and Axes
when working with multiple plots our fig and ax objects are arrays of the same dimensions of Figures and Axes, we can pass the Boolean `sharey` or `sharex` that determines if the plots should share the x or y scales 

 - `Axes` used to add axes data to the figure
	 - `ax.plot(x-axis-data, y-axis-data)` axis-data could be a *Series* or a *Set*  
		 - `marker` default is `None`, adds a marker to the data points, list of supported marker shapes is available [here](https://matplotlib.org/stable/api/markers_api.html#module-matplotlib.markers)
		 - `linestyle` default is `'-'` or `'solid'`, list of supported line styles is available [here](https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D.set_linestyle)  
		 - `color` color string, `'r'` stands for red for example
	 - `ax.set_xlabel('label')` set x-axis label (resp. y-axis), can specify a `color` for the label too
	 - `ax.set_title('title')` set plot title
	 - `ax2 = ax.twinx()` allows us to define a second Axis that shares the same x-axis wit `ax` (resp. `twiny`)
		 - `ax.tick_params('y', color='b')` allows us to set customize various properties of the `'x' or 'y'` axis ticks 
	 - `ax.annotate('label', xy=(pd.Timestamp('date-str'),2))` adds an annotation to the plot at the position xy as shown above with Timestamps on the x-axis and floats on the y-axis
		 - `xytext`just like `xy` this parameter designates the position of the text label
		 - `arrowprops` a dictionary that accepts values such as `arrowstyle` that takes a string `'->'` for example and `color`. [More information](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.annotate.html)

