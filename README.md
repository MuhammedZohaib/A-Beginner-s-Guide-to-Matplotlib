# A Beginner's Guide to Matplotlib

> ### **Matplotlib**

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots()

ax.plot(x,y)
plt.show()

# adding a marker to the plot'
# visit https://matplotlib.org/stable/api/markers_api.html'
ax.plot(x, y, marker="o")

# changing the linestyle
ax.plot(x, y, marker="o", linestyle="--")
# visit: https://matplotlib.org/stable/gallery/lines_bars_and_markers/linestyles.html

# changing the line color
ax.plot(x, y, marker="o", linestyle="--", color = 'r')
# setting the plot labels
ax.set_xlabel("This is x label")
ax.set_ylabel("This is y label")
ax.set_title("This is the title")

# small multiples
fig, ax = plt.subplots(3,2)
# this will return an array of subplots which can be indexed for plotting
# this will insure the range on y-axis is same in all subplots
fig, ax = plt.subplots(3,2)
```

### Plotting Time Series Data

```python
fig, ax = plt.subplots()
ax.plot(df.index, df['col'])
ax.set_xlabel("This is x-label")
ax.set_ylabel("This is y-label")
# Using different y-axis
ax2 = ax.twinx()
ax2.plot(df.index, df['col_1']) # different y-axis but same x-axis
ax2.set_ylabel("This is y-label for 2nd plot")
plt.show()

# we can give color to the plots as well as the labels and ticks
ax.tick_params('either x or y', color='color_name')
```

### Adding Annotations

```python
ax.annotate("annotation text", xy=(pd.TimeStamp("yyyy-mm-dd"), 1))

# moving the annotation:
ax.annotate("annotation text", xy=(pd.TimeStamp("yyyy-mm-dd"), 1), xytext=(pd.Timestamp("yyyy-mm-dd"), -0.2))

# adding arrow to connect the annotation and plot point
ax2.annotate(">1 degree", xy=(pd.Timestamp("yyyy-mm-dd"), 1), 
            xytext=(pd.Timestamp("yyyy-mm-dd"), -0.2),
             arrowprops={"arrowstyle": "->", "color":"gray"})
```

### Bar Charts

```python
# simple bar chat
fig, ax = plt.subplots()
ax.bar(x, y)
plt.show()

# rotating the x-tick labels by 90 degree
ax.set_xticklabels(column, rotation=90)

# creating a stacked bar-chart
ax.bar(x1, y)
ax.bar(x2, y, bottom=x1)
ax.bar(x3, y, bottom=x1+x2)

# adding legends
ax.legend()

# showing plot
ax.show()
```

### Histograms

```python
fig, ax = plt.sublplots()
ax.hist(dataframe['column'])
plt.show()

ax.hist(dataframe['column'], label="label for this histogram", bins="number of bins")
# we can also provide a list of bins in bins parameter
ax.hist(dataframe['column'], bins=[20, 40, 60, 80, 100])

# sometimes if we plot multiple variables in a single plot our plot can be
# overlapping so we can change the histogram type so it can be hollow and
# visible
ax.hist(dataframe['column'], bins=[20, 40, 60, 80, 100], histtype="Step")
```

### Statistical Plotting

```python
# Error Plot -- 1
fig, ax = plt.subplots()

ax.bar("Rowing", mens_rowing['Height'].mean(), yerr=mens_rowing['Height'].std())
ax.bar("Gymnastics", mens_gymnastics['Height'].mean(), yerr=mens_gymnastics['Height'].std())
ax.set_ylabel("Height (cm)")
plt.show()

# Error Plot -- 2
fig, ax = plt.subplots()
ax.errorbar(seattle_weather['MONTH'], seattle_weather['MLY-TAVG-NORMAL'], yerr=seattle_weather['MLY-TAVG-STDDEV'])
ax.errorbar(austin_weather['MONTH'], austin_weather['MLY-TAVG-NORMAL'], yerr=austin_weather['MLY-TAVG-STDDEV'])
ax.set_ylabel("Temperature (Fahrenheit)")
plt.show()

# Error Plot -- 3 (Box Plot)
fig, ax = plt.subplots()
ax.boxplot([mens_rowing['Height'], mens_gymnastics['Height']])
ax.set_xticklabels(["Rowing", "Gymnastics"])
ax.set_ylabel("Height (cm)")
plt.show()
```

### Scatter Plot

```python
fig, ax = plt.subplots()
ax.scatter(climate_change['co2'], climate_change['relative_temp'])
ax.set_xlabel("CO2 (ppm)")
ax.set_ylabel("Relative temperature (C)")
plt.show()

# giving time index to scatter plot as c param
fig, ax = plt.subplots()
ax.scatter(climate_change['co2'], climate_change['relative_temp'], c=climate_change.index)
ax.set_xlabel("CO2 (ppm)")
ax.set_ylabel("Relative temperature (C)")
plt.show()
```

### Changing Plot Style in Matplotlib

```python
plt.style.use("ggplot")
plt.style.use("default")
plt.style.use("bmh")
plt.style.use("seaborn-colorblind")
plt.style.use("tableau-colorblind10")
plt.style.use("grayscale")
plt.style.use("Solarize_Light2")
```

### Saving Matplotlib Plots

```python
fig.savefig("Name_of_plot.png")
fig.savefig("Name_of_plot.jpg")
fig.savefig("Name_of_plot.jpg", quality=50) # 50% quality
fig.savefig("Name_of_plot.svg")
fig.savefig("Name_of_plot.png", dpi=300)

# controlling the size of the figure
fig.set_size_inches([5,3]) # [width, height]


# plot pipeline example:
fig, ax = plt.subplots()
for sport in sports:
  sport_df = summer_2016_medals[summer_2016_medals['Sport'] == sport]
  ax.bar(sport, sport_df["Weight"].mean(), yerr=sport_df["Weight"].std())

ax.set_ylabel("Weight")
ax.set_xticklabels(sports, rotation=90)
fig.savefig("sports_weights.png")
```

---
