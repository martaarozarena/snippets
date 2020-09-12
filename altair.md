# Overview

## Bar chart

```python
trend_bar = alt.Chart(trends).mark_bar().encode(
    x='search_term',
    y='value',
    color='search_term'
)
```

## Line chart
```
trend_line = alt.Chart(trends).mark_line().encode(
    x='yearmonth(date):T',
    y='mean(value)',
    color='search_term'
)
```


## Scatter
```
scatter_brain_body = alt.Chart(brain).mark_circle().encode( 
x='Body Weight', 
y='Brain Weight' 
)
```

## Map
```
url = "https://raw.githubusercontent.com/datasets/geo-countries/master/data/countries.geojson" 
data_geojson_remote = alt.Data(url=url, format=alt.DataFormat(property='features',type='json')) 

# chart object 
alt.Chart(data_geojson_remote).mark_geoshape( 
).encode( 
color="properties.name:N" 
).properties( 
projection={'type': 'identity', 'reflectY': True} 
)
```

## Histogram
```
hist_body = alt.Chart(brain).mark_bar().encode(
x=alt.X('Body Weight',bin=alt.Bin(maxbins=100)), 
y="count()" 
).properties( 
width=300, 
height=150, 
title="Relación peso del cerebro y del cuerpo" 
)
```

## Horizontal composition
```
hist_brain|hist_body
```

## Vertical composition
```
trend_line&trend_line2
```

## Single selection
```
select_term = alt.selection(type="single",encodings=["x"]) 

trend_line = alt.Chart(trends).mark_line().encode( 
x="yearmonth(date):T", 
y="mean(value)", 
color="search_term" 
).transform_filter( 
select_term 
) 

trend_bar = alt.Chart(trends).mark_bar().encode( 
x="search_term", 
y="value", 
color="search_term", 
tooltip="search_term" 
).properties( 
selection=select_term 
) 
```

## Interval selection
```
select_date = alt.selection(type="interval", encodings=["x"]) 

trend_line = alt.Chart(trends).mark_line().encode( 
x="yearmonth(date):T", 
y="mean(value)", 
color="search_term" 
).properties(
    selection=select_date,
)

trend_bar = alt.Chart(trends).mark_bar().encode( 
x="search_term", 
y="value", 
color="search_term", 
tooltip="search_term" 
).transform_filter(
    select_date
)
```
