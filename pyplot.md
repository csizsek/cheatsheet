#Pyplot Cheat Sheet

###Pyplot Basics
Expression | Description
---  | ---
`plt.plot(x)` | Plot `x` as a line plot
`plt.hist(x)` | Plot `x` as a histogram
`plt.scatter(x, y)` | Scatter plot `x` and `y`
`plt.boxplot(x)` | Box plot
`plt.subplot(2, 1, 1)` | Create a figure and select a subplot (nrows, ncols, idx) for plotting points
`plt.plot(x, 'r', y, 'b')` | Plot two data sets on the same graph
`fig = matplotlib.pyplot.gcf()` | Get current figure
`fig.set_size_inches(18.5, 10.5)` | Set the size of a figure
`plt.savefig('graph.png')` | Save plot to file

###Pyplot Styling
Expression | Description
---  | ---
`plt.plot(x, color='g')` | Plot `x` as a line plot with a green line
`plt.plot(x, linestyle='--')` | Plot `x` as a line plot with a dashed line
`plt.plot(x, marker='+')` | Plot `x` as a line plot with markers at the data points
`plt.plot(x, 'g--')` | Plot `x` as a line plot with a green dashed line
`plt.plot(x, 'ro-')` | Plot `x` as a line plot with a red continuous line and dots at the data
`plt.ylabel('hello')` | Set axis labels
`plt.xlim(5, 10)` | Set axis limits
`plt.title('Foo')` | Set title
`plt.legend((p[0], p[1]), ("foo", "bar"))` | Set legend for lines saved in `p`
`plt.xticks(np.arange(0, 500, 20))` | Set ticks along an axis
`plt.grid()` | Set grid