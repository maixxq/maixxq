---
title: Let's get data rocking
date: 2020-04-15 20:47:18
excerpt: Noting down the "data" nuggets I learned from everywhere so that I can better understand and use the data in the world! 
type: post
blog: true
---

Data has been fanscinating to me. Similar to technology, it gives us the potential to do so many things. From the process of collecting data to drawing insights based on the data, we can get an overview of the situation and perhaps find new approaches in solving certain problems. Commonly used tools for data - Python, R, SQL, Tableau and many many more.

## CSV - Common Separated Values

It means what it is being called. CSV is a file with values separated by commas. 
Many libraries exist to visualize and analyse data. Before diving into a data visualization project, these libraries come in handy and allow us to make beautiful data visualization. 

To set up coding environment,

```js
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
//This is to check everything is been imported and loaded
print("Done!")
```

To read a CSV file and the the dataset,

```js
//It's important to locate the right path to read!
read_filepath = "../input/filename.csv"

// Create a variable that read the CSV file
var_name = pd.read_csv(read_filepath)

```

To examine the first and last few columns of the dataset using the variable created

```js
// The first 5 rows of the data will be printed
var_name.head()
// The last 5 rows of the data will be printed
var_name.tail()
```

