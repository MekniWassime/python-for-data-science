   

> Seaborn is **a Python data visualization library based on matplotlib**. It provides a high-level interface for drawing attractive and informative statistical graphics.

    import seaborn as sns
    
for most of the plots shown below we can omit the `data` variable and use lists of data directly instead of column names but we are going to focus on syntaxes using *DataFrame*s and the `data` parameter
#### Relational Plots
 - `sns.scatterplot(x='col1-name', y='col2-name', data=df)` render a scatter plot which shows values from `'col1'` against `'col2'` from `df`
	 - `hue` column name or list of values, associates a color to each unique value and colors each point based on the corresponding `hue` value and add a legend to the graph automatically
	 - `hue_order` list of values, allows you to set the order of unique values of hue by specifying them in the wanted order
	 - `palette` a dictionary that maps each unique hue value to a color. in other words, a dictionary of hue values as keys and colors as values
	 - `size` column name or list of values, change the size of the data-points based on the values
	 - `alpha` value between 0 and 1 sets the opacity of values
	 - `style` column name or list of values, just like hue but change point style instead of color
	 
 - `sns.relplot(x='col1', y='col2', data=df, kind='scatter')` relplot stands for relational plots which countrary to scatter plots that use colors to divide data into subgroups, relplot makes a plot for each subgroup
	 - `kind` either `'scatter'` or `'line'`
	 - `col` column name or list of values used to divide data-points into subgroups, subplots will be laid out horizontally
	 - `row` divide data-points into subgroups just like `col` but the plots are laid out vertically, both options can be used simultaneously resulting in a matrix like structure
	 -  `col_wrap` integer, set the maximum number of columns per each line
	 - `col_order` specify the order each of the unique values of `'col'` will be laid out on (resp `row_order`)
	 - `hue`, `palette`, `style`, `size` and `aplha` are also supported
	 - if `kind` is set to `'line'`
		 - `marker` default is False, if set to True show a marker for each data-point, markers are affected by `style` and `hue` parameters
		 - `dashes` default is True, if set to False lines are not affected by the `style` parameter and will all be solid lines, markers are still affected
		 - if x-axis points have more than a single observation lines will go through the average values for each x value. The `ci` (confidence interval) parameter is used to specify additional statistical informations like confidence intervals (`ci='ci'` default), standart deviation (`ci='sd'`) or `ci=None` to just show the average lines
 #### Categorical Plots
 - `sns.countplot(x='col-name', data=df)` could either use `x` or `y` to choose on which axis the bars emerge from, counts the number of each value and shows a bar for each unique value
	 - `hue` column name or list of values used to divide each bar into a subgroup based on the unique values of `hue`, also supports `hue_order` and `palette`
 - `sns.catplot(x='col-name', data=df, kind='count')` if `kind` is set to `'count'` this renders a count plot
	 - `order` list of unique `'col'` values in the desired order
 - `sns.catplot(x='col1', y='col2', data=df, kind='bar')` if `kind` is set to `'bar'` this renders a bar plot
	 - will autodetect the categorical data and that's the axis where the bars will emerge from, if the values are Boolean it will show the percentage of True values in each category
	 - `ci` default value is `'ci'` can be set to `'sd'` for standard deviation or `None` to disable them
 - `sns.catplot(x='co1', y='col2', data=df, kind='point')` similar to bar plots
	 - `join` default is True, if set to False disable the lines between points
	 - `estimator` default is `mean` can be set to `median` function imported from numpy
	 - `capsize` disabled by default, can be set to the desired cap width, `0.2` for example
 - `sns.catplot(x='col1', y='col2', data=df, kind='box')` this will render a box plot
	 - `sym` if set to `""`, outliers are going to be ignored
	 - `whis` default is `1.5` could be set to a float or a list of two floats, `whis=[0,100]` makes it so that the upper whisker shows the maximum value and the lower whisker shows the minimum value
	 - `hue`, `col_order`, `row_order` and the parameters related to them are available for box plots 
### Plot Styles

    sns.set_style('style')
available styles are `'white'` (default), `'dark'`, `'whitegrid'`, `darkgrid` or `'ticks'`

    sns.set_palette(color-palette)
for a list of color palettes go [here](https://seaborn.pydata.org/tutorial/color_palettes.html), or we can use a list of color strings or html hex colors `'#FBB4AE'` to define our own palettes

    sns.set_context('context')
set the scale of the plot, options are `'paper'` default, `'notebook'`, `talk` or `'poster'`. For example we use `'talk'` to make it easier for viewers from far away to read the plot
### Customizing Plots

`relplot` and `catplot` create a *FacetGrid* object, single plot functions like `scatterplot` or `countplot` produce *AxesSubplot* objects, we can assign the return value of these functions like so

    g = sns.relplot(...)

 - *FacetGrid*s
	 - `g.fig.suptitle('title')` adds a title to the figure, we can use `y` parameter defaults to `1` to control the vertical position of the title
	 - `g.set_titles('this is {col_name}')` sets the title of individual subplots where `{col_name}` is replaced by the value of the plot's `col` argument 
	 -`g.set(xlabel='label1', ylabel='label2')` set the x and y axis labels 
	 
 - *AxesSubplot*s
	 - `g.set_title('title')` adds a title to the figure and `y` can be used to control the position of the title
	 - `g.set(xlabel='label1', ylabel='label2')` set the x and y axis labels
 - to rotate x ticks we use the matplotlib function `plt.xticks(rotation=90)`

