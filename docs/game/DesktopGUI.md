# Desktop GUI for designers
We plan to develop an app for everything, including AI Module, Unity frontend, python gameplay, card/deck editing, data visualization, etc.
## Motivations
### Accessible to designers
 After half, we start to think about how to help designers. We need a user friendly GUI to let designers use all the tools we provide.
### Organize our tools chain
 We have many tools in different platforms using different techniques. When we try to build more and more tools, it is a chance to organize our tool chain.  


## Schemes
We have sevarl choices to develop our desktop GUI
### Unity Built-in UI System
#### Pros
 Our game GUI is developed in Unity, and we are familiar with Unity!
#### Cons
 Unity’s UI system is not designed for generalized desktop GUI. This would be a big problem when we try to build complex UI such as data visualization.
### Browser + HTML + CSS + JS 
#### Pros
Easy to use, only need a browser. Easy to develop, web techniques are convenient and have many libraries and frameworks.
#### Cons
Browsers usually don’t support manipulating local files and start other .exe in another process, which are important to us.

### Electron(final choice)
We finnal chose electron for several reasons:
- Use web standards:       
Developing a desktop app is basically the same as writing a website in electron. It uses html, javascript and css, and we are already familiar with these techniques. 
- Highlevel, lightweight:       
Because of html and javascript, developing an app is much easier than other techniques such as windows naive API, Qt, etc. 