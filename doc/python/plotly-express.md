---
jupyter:
  jupytext:
    notebook_metadata_filter: all
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.2'
      jupytext_version: 1.4.2
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.7.7
  plotly:
    description: Plotly Express is a terse, consistent, high-level API for creating
      figures.
    display_as: file_settings
    language: python
    layout: base
    name: Plotly Express
    order: 4
    page_type: example_index
    permalink: python/plotly-express/
    thumbnail: thumbnail/plotly-express.png
---

### Overview

The `plotly.express` module (usually imported as `px`) contains functions that can create entire figures at once, and is referred to as Plotly Express or PX. Plotly Express is a built-in part of the `plotly` library, and is the recommended starting point for creating most common figures. Every Plotly Express function uses [graph objects](/python/graph-objects/) internally and returns a `plotly.graph_objects.Figure` instance. Throughout the `plotly` documentation, you will find the Plotly Express way of building figures at the top of any applicable page, followed by a section on how to use graph objects to build similar figures. Any figure created in a single function call with Plotly Express could be created using graph objects alone, but with between 5 and 100 times more code.

Plotly Express provides [more than 30 functions for creating different types of figures](https://plotly.com/python-api-reference/plotly.express.html). The API for these functions was carefully designed to be as consistent and easy to learn as possible, making it easy to switch from a scatter plot to a bar chart to a histogram to a sunburst chart throughout a data exploration session. *Scroll down for a gallery of Plotly Express plots, each made in a single function call.*

Plotly Express currently includes the following functions:

* **Basics**: [`scatter`](/python/line-and-scatter/), [`line`](/python/line-charts/), [`area`](/python/filled-area-plots/), [`bar`](/python/bar-charts/), [`funnel`](/python/funnel-charts/)
* **Part-of-Whole**: [`pie`](/python/pie-charts/), [`sunburst`](/python/sunburst-charts/), [`treemap`](/python/treemaps/), [`funnel_area`](/python/funnel-charts/)
* **1D Distributions**: [`histogram`](/python/histograms/), [`box`](/python/box-plots/), [`violin`](/python/violin/), `strip`
* **2D Distributions**: [`density_heatmap`](/python/2D-Histogram/), [`density_contour`](/python/2d-histogram-contour/)
* **Matrix Input**: [`imshow`](/python/imshow/)
* **3-Dimensional**: [`scatter_3d`](/python/3d-scatter-plots/), [`line_3d`](/python/3d-line-plots/)
* **Multidimensional**: [`scatter_matrix`](/python/splom/), [`parallel_coordinates`](/python/parallel-coordinates-plot/), [`parallel_categories`](/python/parallel-categories-diagram/)
* **Tile Maps**: [`scatter_mapbox`](/python/scattermapbox/), [`line_mapbox`](/python/lines-on-mapbox/), [`choropleth_mapbox`](/python/mapbox-county-choropleth/), [`density_mapbox`](/python/mapbox-density-heatmaps/)
* **Outline Maps**: [`scatter_geo`](/python/scatter-plots-on-maps/), [`line_geo`](/python/lines-on-maps/), [`choropleth`](/python/choropleth-maps/)
* **Polar Charts**: [`scatter_polar`](/python/polar-chart/), [`line_polar`](/python/polar-chart/), [`bar_polar`](/python/wind-rose-charts/)
* **Ternary Charts**: [`scatter_ternary`](/python/ternary-plots/), [`line_ternary`](/python/ternary-plots/)

### High-Level Features

The Plotly Express API in general offers the following features:

* **A single entry point into `plotly`**: just `import plotly.express as px` and get access to [all the plotting functions](https://plotly.com/python-api-reference/plotly.express.html), plus [built-in demo datasets under `px.data`](https://plotly.com/python-api-reference/generated/plotly.data.html#module-plotly.data) and [built-in color scales and sequences under `px.color`](https://plotly.com/python-api-reference/generated/plotly.colors.html#module-plotly.colors). Every PX function returns a `plotly.graph_objects.Figure` object, so you can edit it using all the same methods like [`update_layout` and `add_trace`](https://plotly.com/python/creating-and-updating-figures/#updating-figures).
* **Sensible, Overrideable Defaults**: PX functions will infer sensible defaults wherever possible, and will always let you override them.
* **Flexible Input Formats**: PX functions [accept input in a variety of formats](/python/px-arguments/), from `list`s and `dict`s to [long-form or wide-form Pandas `DataFrame`s](/python/wide-form/) to [`numpy` arrays and `xarrays`](/python/imshow/) to [GeoPandas `GeoDataFrames`](/python/maps/).
* **Automatic Trace and Layout configuration**: PX functions will create one [trace](/python/figure-structure) per animation frame for each unique combination of data values mapped to discrete color, symbol, line-dash, facet-row and/or facet-column. Traces' `legendgroup` and `showlegend` attributed are set such that only one legend item appears per unique combination of discrete color, symbol and/or line-dash. Traces are automatically linked to a correctly-configured [subplot of the appropriate type](/python/figure-structure).
* **Automatic Figure Labelling**: PX functions label axes, legends and colorbars based in the input `DataFrame` or `xarray`, and provide [extra control with the `labels` argument](/python/styling-plotly-express/).
* **Automatic Hover Labels**: PX functions populate the hover-label using the labels mentioned above, and provide [extra control with the `hover_name` and `hover_data` arguments](/python/hover-text-and-formatting/).
* **Styling Control**: PX functions [read styling information from the default figure template](/python/styling-plotly-express/), and support commonly-needed [cosmetic controls like `category_orders` and `color_discrete_map`](/python/styling-plotly-express/) to precisely control categorical variables.
* **Uniform Color Handling**: PX functions automatically switch between [continuous](/python/colorscales/) and [categorical color](/python/discrete-color/) based on the input type.
* **Faceting**: the 2D-cartesian plotting functions support [row, column and wrapped facetting with `facet_row`, `facet_col` and `facet_col_wrap` arguments](/python/facet-plots/).
* **Marginal Plots**: the 2D-cartesian plotting functions support marginal distribution plots with the `marginal`, `marginal_x` and `marginal_y` arguments.
* **A Pandas backend**: the 2D-cartesian plotting functions are available as [a Pandas plotting backend](/python/pandas-backend/) so you can call them via `df.plot()`.
* **Trendlines**: `px.scatter` supports [built-in trendlines with accessible model output](/python/linear-fits/).
* **Animations**: many PX functions support [simple animation support via the `animation_frame` and `animation_group` arguments](/python/animations/).

### Gallery

The following set of figures is just a sampling of what can be done with Plotly Express.

#### Scatter, Line, Area and Bar Charts

**Read more about [scatter plots](/python/line-and-scatter/) and [discrete color](/python/discrete-color/).**

```python
import plotly.express as px
df = px.data.iris()
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species")
fig.show()
```

**Read more about [trendlines](/python/linear-fits/) and [templates](/python/templates/).**

```python
import plotly.express as px
df = px.data.iris()
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species", marginal_y="violin",
           marginal_x="box", trendline="ols", template="simple_white")
fig.show()
```

**Read more about [error bars](/python/error-bars/).**

```python
import plotly.express as px
df = px.data.iris()
df["e"] = df["sepal_width"]/100
fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species", error_x="e", error_y="e")
fig.show()
```

**Read more about [bar charts](/python/bar-charts/).**

```python
import plotly.express as px
df = px.data.tips()
fig = px.bar(df, x="sex", y="total_bill", color="smoker", barmode="group")
fig.show()
```

**Read more about [facet plots](/python/facet-plots/).**

```python
import plotly.express as px
df = px.data.tips()
fig = px.bar(df, x="sex", y="total_bill", color="smoker", barmode="group", facet_row="time", facet_col="day",
       category_orders={"day": ["Thur", "Fri", "Sat", "Sun"], "time": ["Lunch", "Dinner"]})
fig.show()
```

**Read more about [scatterplot matrices (SPLOMs)](/python/splom/).**


```python
import plotly.express as px
df = px.data.iris()
fig = px.scatter_matrix(df, dimensions=["sepal_width", "sepal_length", "petal_width", "petal_length"], color="species")
fig.show()
```

**Read more about [parallel coordinates](/python/parallel-coordinates-plot/) and [parallel categories](/python/parallel-categories-diagram/), as well as [continuous color](/python/colorscales/).**

```python
import plotly.express as px
df = px.data.iris()
fig = px.parallel_coordinates(df, color="species_id", labels={"species_id": "Species",
                  "sepal_width": "Sepal Width", "sepal_length": "Sepal Length",
                  "petal_width": "Petal Width", "petal_length": "Petal Length", },
                    color_continuous_scale=px.colors.diverging.Tealrose, color_continuous_midpoint=2)
fig.show()
```

```python
import plotly.express as px
df = px.data.tips()
fig = px.parallel_categories(df, color="size", color_continuous_scale=px.colors.sequential.Inferno)
fig.show()
```

**Read more about [hover labels](/python/hover-text-and-formatting/).**

```python
import plotly.express as px
df = px.data.gapminder()
fig = px.scatter(df.query("year==2007"), x="gdpPercap", y="lifeExp", size="pop", color="continent",
           hover_name="country", log_x=True, size_max=60)
fig.show()
```

**Read more about [animations](/python/animations/).**

```python
import plotly.express as px
df = px.data.gapminder()
fig = px.scatter(df, x="gdpPercap", y="lifeExp", animation_frame="year", animation_group="country",
           size="pop", color="continent", hover_name="country", facet_col="continent",
           log_x=True, size_max=45, range_x=[100,100000], range_y=[25,90])
fig.show()
```

**Read more about [line charts](/python/line-charts/).**

```python
import plotly.express as px
df = px.data.gapminder()
fig = px.line(df, x="year", y="lifeExp", color="continent", line_group="country", hover_name="country",
        line_shape="spline", render_mode="svg")
fig.show()
```

**Read more about [area charts](/python/filled-area-plots/).**

```python
import plotly.express as px
df = px.data.gapminder()
fig = px.area(df, x="year", y="pop", color="continent", line_group="country")
fig.show()
```

### Part to Whole Charts

**Read more about [pie charts](/python/pie-charts/).**

```python
import plotly.express as px
df = px.data.gapminder().query("year == 2007").query("continent == 'Europe'")
df.loc[df['pop'] < 2.e6, 'country'] = 'Other countries' # Represent only large countries
fig = px.pie(df, values='pop', names='country', title='Population of European continent')
fig.show()
```

**Read more about [sunburst charts](/python/sunburst-charts/).**

```python
import plotly.express as px

df = px.data.gapminder().query("year == 2007")
fig = px.sunburst(df, path=['continent', 'country'], values='pop',
                  color='lifeExp', hover_data=['iso_alpha'])
fig.show()
```

**Read more about [treemaps](/python/treemaps/).**

```python
import plotly.express as px
import numpy as np
df = px.data.gapminder().query("year == 2007")
fig = px.treemap(df, path=[px.Constant('world'), 'continent', 'country'], values='pop',
                  color='lifeExp', hover_data=['iso_alpha'])
fig.show()
```

#### Distributions

**Read more about [histograms](/python/histograms/).**

```python
import plotly.express as px
df = px.data.tips()
fig = px.histogram(df, x="total_bill", y="tip", color="sex", marginal="rug", hover_data=df.columns)
fig.show()
```

**Read more about [box plots](/python/box-plots/).**

```python
import plotly.express as px
df = px.data.tips()
fig = px.box(df, x="day", y="total_bill", color="smoker", notched=True)
fig.show()
```

**Read more about [violin plots](/python/violin/).**

```python
import plotly.express as px
df = px.data.tips()
fig = px.violin(df, y="tip", x="smoker", color="sex", box=True, points="all", hover_data=df.columns)
fig.show()
```

```python
import plotly.express as px
df = px.data.tips()
fig = px.strip(df, x="total_bill", y="time", orientation="h", color="smoker")
fig.show()
```

**Read more about [density contours, also known as 2D histogram contours](/python/2d-histogram-contour/).**

```python
import plotly.express as px
df = px.data.iris()
fig = px.density_contour(df, x="sepal_width", y="sepal_length")
fig.show()
```

```python
import plotly.express as px
df = px.data.iris()
fig = px.density_contour(df, x="sepal_width", y="sepal_length", color="species", marginal_x="rug", marginal_y="histogram")
fig.show()
```

**Read more about [density heatmaps, also known as 2D histograms](/python/2D-Histogram/).**

```python
import plotly.express as px
df = px.data.iris()
fig = px.density_heatmap(df, x="sepal_width", y="sepal_length", marginal_x="rug", marginal_y="histogram")
fig.show()
```

### Images and Heatmaps

**Read more about [heatmaps and images](/python/imshow/).**

```python
import plotly.express as px

fig = px.imshow([[1, 20, 30],
                 [20, 1, 60],
                 [30, 60, 1]])
fig.show()
```

```python
import plotly.express as px
import numpy as np
img_rgb = np.array([[[255, 0, 0], [0, 255, 0], [0, 0, 255]],
                    [[0, 255, 0], [0, 0, 255], [255, 0, 0]]
                   ], dtype=np.uint8)
fig = px.imshow(img_rgb)
fig.show()
```

#### Maps

**Read more about [tile maps](/python/mapbox-layers/) and [point on tile maps](/python/scattermapbox/).**

```python
import plotly.express as px
df = px.data.carshare()
fig = px.scatter_mapbox(df, lat="centroid_lat", lon="centroid_lon", color="peak_hour", size="car_hours",
                  color_continuous_scale=px.colors.cyclical.IceFire, size_max=15, zoom=10,
                  mapbox_style="carto-positron")
fig.show()
```

**Read more about [tile map GeoJSON choropleths](/python/mapbox-county-choropleth/).**

```python
import plotly.express as px

df = px.data.election()
geojson = px.data.election_geojson()

fig = px.choropleth_mapbox(df, geojson=geojson, color="Bergeron",
                           locations="district", featureidkey="properties.district",
                           center={"lat": 45.5517, "lon": -73.7073},
                           mapbox_style="carto-positron", zoom=9)
fig.show()
```

**Read more about [outline symbol maps](/python/scatter-plots-on-maps/).**

```python
import plotly.express as px
df = px.data.gapminder()
fig = px.scatter_geo(df, locations="iso_alpha", color="continent", hover_name="country", size="pop",
               animation_frame="year", projection="natural earth")
fig.show()
```


**Read more about [choropleth maps](/python/choropleth-maps/).**

```python
import plotly.express as px
df = px.data.gapminder()
fig = px.choropleth(df, locations="iso_alpha", color="lifeExp", hover_name="country", animation_frame="year", range_color=[20,80])
fig.show()
```


#### Polar Coordinates

**Read more about [polar plots](/python/polar-chart/).**

```python
import plotly.express as px
df = px.data.wind()
fig = px.scatter_polar(df, r="frequency", theta="direction", color="strength", symbol="strength",
            color_discrete_sequence=px.colors.sequential.Plasma_r)
fig.show()
```

**Read more about [radar charts](https://plotly.com/python/radar-chart/).**

```python
import plotly.express as px
df = px.data.wind()
fig = px.line_polar(df, r="frequency", theta="direction", color="strength", line_close=True,
            color_discrete_sequence=px.colors.sequential.Plasma_r)
fig.show()
```

**Read more about [polar bar charts](/python/wind-rose-charts/).**

```python
import plotly.express as px
df = px.data.wind()
fig = px.bar_polar(df, r="frequency", theta="direction", color="strength", template="plotly_dark",
            color_discrete_sequence= px.colors.sequential.Plasma_r)
fig.show()
```

#### 3D Coordinates

**Read more about [3D scatter plots](/python/3d-scatter-plots/).**

```python
import plotly.express as px
df = px.data.election()
fig = px.scatter_3d(df, x="Joly", y="Coderre", z="Bergeron", color="winner", size="total", hover_name="district",
                  symbol="result", color_discrete_map = {"Joly": "blue", "Bergeron": "green", "Coderre":"red"})
fig.show()
```

#### Ternary Coordinates

**Read more about [ternary charts](/python/ternary-plots/).**

```python
import plotly.express as px
df = px.data.election()
fig = px.scatter_ternary(df, a="Joly", b="Coderre", c="Bergeron", color="winner", size="total", hover_name="district",
                   size_max=15, color_discrete_map = {"Joly": "blue", "Bergeron": "green", "Coderre":"red"} )
fig.show()
```
