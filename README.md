
# Python For loops Lab

### Learning Objectives

* Understand how for loops can help us reduce repetition
* Understand the syntax of for loops 

### Picking up where we last left off

In the last lesson, we worked with some of our travel data.  Let's retrieve a list with our travel information again from excel.  First, we read the information from excel as a list of dictionaries, with each dictionary representing a location.  And we assign this list to the variable `cities`.


```python
import pandas
file_name = './cities.xlsx'
travel_df = pandas.read_excel(file_name)
cities = travel_df.to_dict('records')
```

Next, we retrieve the first three city names, stored as the `'City'` attribute of each dictionary, and `'Population'` of each of the cities.  Then we plot the names as our `x_values` and the populations as our `y_values`.


```python
import plotly

plotly.offline.init_notebook_mode(connected=True)

x_values = [cities[0]['City'], cities[1]['City'], cities[2]['City']]
y_values = [cities[0]['Population'], cities[1]['Population'], cities[2]['Population']]
trace_first_three_pops = {'x': x_values, 'y': y_values, 'type': 'bar'}
plotly.offline.iplot([trace_first_three_pops])
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



<div id="abb4d826-04bc-4fa0-b2ec-b3c61d6b4423" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("abb4d826-04bc-4fa0-b2ec-b3c61d6b4423", [{"x": ["Buenos Aires", "Toronto", "Marakesh"], "y": [2891, 2732, 929], "type": "bar", "uid": "3508c154-c9ca-11e9-96c8-3af9d3ad3e0b"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Of course, as you may have spotted, there is a good amount of repetition in displaying this data.  Just take a look at how we retrieved the data for our `x_values` and `y_values`.  


```python
x_values = [cities[0]['City'], cities[1]['City'], cities[2]['City']]
y_values = [cities[0]['Population'], cities[1]['Population'], cities[2]['Population']]
```

So in this lesson, we will use our `for` loop to display information about our travel locations with less repetition.

### Working with the For Loop

Our `cities` list contains information about the top 12 cities by population.  For our upcoming iteration tasks, it will be useful to have a list of the numbers 0 through 11.  Use what we know about `len` and `range`to generate a list of numbers 0 through 11.  Assign this to a variable called `city_indices`.


```python
city_indices = list(range(len(cities)))
city_indices # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]



Now we want to create labels for each of the cities. We'll provide a list of the `city_names` for you. 


```python
city_names = ['Buenos Aires',
 'Toronto',
 'Marakesh',
 'Albuquerque',
 'Los Cabos',
 'Greenville',
 'Archipelago Sea',
 'Pyeongchang',
 'Walla Walla Valley',
 'Salina Island',
 'Solta',
 'Iguazu Falls']
```

Your task is to assign the variable `names_and_ranks` to a list, with each element equal to the city name and it's corresponding rank.  For example, the first element would be, `"1. Buenos Aires"` and the second would be `"2. Toronto"`.  Use a `for` loop and the lists `city_indices` and `city_names` to accomplish this.  We'll need to perform some nifty string interpolation to format our strings properly.  Check out [f-string interpolation](https://www.programiz.com/python-programming/string-interpolation#f) to see how we can pass values into a string.  Remember that list indices start at zero, but we want our `names_and_ranks` list to start at one!


```python
names_and_ranks = []
for index in city_indices: 
    names_and_ranks.append(f"{index + 1}. {city_names[index]}")
    
names_and_ranks
    
    # make sure the list is empty
```




    ['1. Buenos Aires',
     '2. Toronto',
     '3. Marakesh',
     '4. Albuquerque',
     '5. Los Cabos',
     '6. Greenville',
     '7. Archipelago Sea',
     '8. Pyeongchang',
     '9. Walla Walla Valley',
     '10. Salina Island',
     '11. Solta',
     '12. Iguazu Falls']




```python
print(names_and_ranks[0]) # '1. Buenos Aires'
print(names_and_ranks[1]) # '2. Toronto'
print(names_and_ranks[-1]) # '12. Iguazu Falls'
```

    1. Buenos Aires
    2. Toronto
    12. Iguazu Falls


Ok, now let's create a new variable called `city_populations`.  Use a `for` loop to iterate through `cities` and have `city_populations` equal to each of the populations.


```python
city_populations = []
for city in cities:
    city_populations.append(city['Population'])
city_populations
```




    [2891, 2732, 929, 559, 288, 93, 60, 44, 33, 3, 2, 0]




```python
print(city_populations[0]) # 2891
print(city_populations[1]) # 2732
print(city_populations[-1])# 0
```

    2891
    2732
    0


Great! Now we can begin to plot this data.  First, let's create a trace of our populations and set it to the variable `trace_populations`.


```python
trace_populations = {'x': names_and_ranks, 
                     'y': city_populations, 
                     'text': names_and_ranks, 
                     'type': 'bar', 
                     'name': 'populations'}
```


```python
import plotly
plotly.offline.init_notebook_mode(connected=True)
plotly.offline.iplot([trace_populations])
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



<div id="7abd61b0-4da0-4c40-a667-7679f5b714f0" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("7abd61b0-4da0-4c40-a667-7679f5b714f0", [{"name": "populations", "text": ["1. Buenos Aires", "2. Toronto", "3. Marakesh", "4. Albuquerque", "5. Los Cabos", "6. Greenville", "7. Archipelago Sea", "8. Pyeongchang", "9. Walla Walla Valley", "10. Salina Island", "11. Solta", "12. Iguazu Falls"], "x": ["1. Buenos Aires", "2. Toronto", "3. Marakesh", "4. Albuquerque", "5. Los Cabos", "6. Greenville", "7. Archipelago Sea", "8. Pyeongchang", "9. Walla Walla Valley", "10. Salina Island", "11. Solta", "12. Iguazu Falls"], "y": [2891, 2732, 929, 559, 288, 93, 60, 44, 33, 3, 2, 0], "type": "bar", "uid": "44f0a8e8-c9ca-11e9-bab9-3af9d3ad3e0b"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


Now we want declare a variable called `city_areas` that points to a list of all of the areas of the cities.  Let's use a `for` loop to iterate through our `cities` and have `city_areas` equal to each area of the city.  


```python
city_areas = []
for city in cities:
    city_areas.append(city['Area'])
city_areas
```




    [203, 630, 230, 491, 3751, 68, 2000, 1464, 35, 26, 59, 2396]




```python
trace_areas = {'x': names_and_ranks, 'y': city_areas, 'text': names_and_ranks, 'type': 'bar', 'name': 'areas'}
```


```python
import plotly
plotly.offline.init_notebook_mode(connected=True)
plotly.offline.iplot([trace_populations, trace_areas])
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



<div id="31389960-ff02-458b-8c51-b868704d8e58" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("31389960-ff02-458b-8c51-b868704d8e58", [{"name": "populations", "text": ["1. Buenos Aires", "2. Toronto", "3. Marakesh", "4. Albuquerque", "5. Los Cabos", "6. Greenville", "7. Archipelago Sea", "8. Pyeongchang", "9. Walla Walla Valley", "10. Salina Island", "11. Solta", "12. Iguazu Falls"], "x": ["1. Buenos Aires", "2. Toronto", "3. Marakesh", "4. Albuquerque", "5. Los Cabos", "6. Greenville", "7. Archipelago Sea", "8. Pyeongchang", "9. Walla Walla Valley", "10. Salina Island", "11. Solta", "12. Iguazu Falls"], "y": [2891, 2732, 929, 559, 288, 93, 60, 44, 33, 3, 2, 0], "type": "bar", "uid": "9a44396c-c9cb-11e9-995f-3af9d3ad3e0b"}, {"name": "areas", "text": ["1. Buenos Aires", "2. Toronto", "3. Marakesh", "4. Albuquerque", "5. Los Cabos", "6. Greenville", "7. Archipelago Sea", "8. Pyeongchang", "9. Walla Walla Valley", "10. Salina Island", "11. Solta", "12. Iguazu Falls"], "x": ["1. Buenos Aires", "2. Toronto", "3. Marakesh", "4. Albuquerque", "5. Los Cabos", "6. Greenville", "7. Archipelago Sea", "8. Pyeongchang", "9. Walla Walla Valley", "10. Salina Island", "11. Solta", "12. Iguazu Falls"], "y": [203, 630, 230, 491, 3751, 68, 2000, 1464, 35, 26, 59, 2396], "type": "bar", "uid": "9a443ac0-c9cb-11e9-b0bd-3af9d3ad3e0b"}], {}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


### Summary

In this section we saw how we can use `for` loops to go through elements of a list and perform the same operation on each.  By using `for` loops we were able to reduce the amount of code that we wrote and while also writing more expressive code.
