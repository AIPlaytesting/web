# Data visualization
Data visualization might be the most important part of this app. However, drawing graphics, especially interactive one, is not as same as that in game engines.
### Naive/Low-level solutions
One solution is draw data graphics by using svg, since html standards support this format. Or we can use some libraries like webGL.  

Even though we can have highly customized graphics to show our data, building a data visualization module from scratch is overscoped because we only have a few weeks to finish the whole app.


### Javascript Data Visualization Library 
Javascript has many data visualization libraries. We finally choose d3.js (https://github.com/d3/d3 ) among others  for 2 reasons:
1. Independent: Many other data visualization libraries( such as Victory, Rechard,etc) only work with some front-end frameworks like React and Vue.  d3.js easter to integrate since it only needs javascript
2. Community resoruces： Many templates and tutorials of d3.js on the internet.