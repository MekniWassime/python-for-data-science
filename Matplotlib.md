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
	 - `ax.bar(x-labels, y-values)` plot a bar graph where each x-label has a bar of height y-value, call this multiple times to draw bar plots ontop of eachother
		 - `bottom` a list of values that are used to offset each bar vertically
		 - `label` string used as a label for the graph, used by `ax.legend()` incase of multiple superimposed bar plots
		 - `yerr` used to add error bars to a plot (error could be the standard deviation for example)
		 - if the labels are overlapping we can rotate them 90° using `ax.set_xticklabels(x-labels, rotation=90)`		 
 - `ax.hist(values, label='label', bins=10)` plots values on a histogram, you can call this multiple times to render multiple histograms
	 - `label` is used by the legend
	 - `bins` is set to 10 by default, you can give it an integer or a list of integers to make a non uniform histogram
	 - `histtype` default is `'bar'` could be set to `'barstacked'`, `'step'` or `'stepfilled'` 
 - `ax.boxplot([values1, ...])` render a boxplot out of a set of values or multiple sets  
 - `ax.errorbar(x-values, y-values, yerr=err-values)` a line plot with error bar at each data point
 - `ax.set_xticklabels(labels)` set the tick labels of the x-axis (reps y-axis)
 - `ax.scatter(x-values, y-values)` render a scatter plot
	 - `c` list of floats, instead of setting a single `color` we can use `c` to create points that are colored depending on values from a list (mainly one of the axis values)
### Exporting figures
 - `plt.style.use('default')` select an overall style, a gallery of styles is availabel [here](https://matplotlib.org/stable/gallery/style_sheets/style_sheets_reference.html)
 - to save a figure as a file, instead of calling `plt.show()` we call `fig.savefig(path.ext)` where we specify file name and it's extension with most popular file types being png, pdf, ps, eps or svg, other parameters can be specified like `quality` a value from 1 to 100 for jpg and `dpi` for png
 - `fig.set_size_inches([4,3])` set the size and aspect ratio of the figure 
