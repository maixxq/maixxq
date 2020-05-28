---
title: Graphing with Chart.js 
date: 2020-05-25 11:11:11
excerpt: After following the tutorial Graphing with Chart.js - Working With Data & APIs in JavaScript by the Coding Train, I have come up with a visualization of the total number of covid-19 cases by country. Daniel is one of the most charismatic lecturer producing wonderful high quality content in his channel Coding Train. This is where I learned about fetch(), async function and javascript library chart.js. 
type: post
blog: true
---

> Data visualization is the graphic representation of data and information.

Visualizing data is a powerful tool, translating data information into meaningful insights. The aim of data visualization is to spot patterns and trends in data sets, allowing us to gain a better understanding of the information. Before turning the data into its graphical representation, data cleaning is an essential stage prior to the actual data processing. In order to ensure working with clean data sets, undesire data inputs such as incomplete, inaccurate and irrelevant records have to be removed or replaced. Once the data is cleaned, it is ready to be translated to visual interpretation. 

In the tutorial, we used an already cleaned data set from NASA. The only 'cleaning' required was to remove the last line of empty input which gives `undefined`. And Voilà, here is the final result! :tada: [NASA Mean Temperature Data](https://maixxq.github.io/coding_train_data_api/data_api/01_temp_data/index.html)

<img src="/temp.jpg" width="600" height="350">

One thing for sure about creating new things is to master the art of reading documentations and applying them to the development itself. Immense amount of patience is needed but it's worth it.

### Fetch API 
> Fetch provides a generic definition of `Request` and `Response` objects

The `fetch()` method returns a `Promise` which resolves the `Response` to the request. Next, different methods will be applied to the retrieved `Response` to identify the body content and how it should be handled. The body content can be in the format of text, blob (image) or JSON (javascript objects notation).

