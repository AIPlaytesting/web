[unity-arc]:resources/unity-arc.png
[unity-render]:resources/unity-render.png
[untiy-animation]:resources/unity-animation.png
# Use Unity To Develop the Player GUI
## Key features of  Unity front-end 
1. **Decoupled front-end** :
Front-end includes all animations, UI, and graphics, but shouldn’t have anything to control the gameplay logic. 
2. **Data-driven rendering**:
Rendering of the game is based on data, just like browsers render the HTML. So when we change game logic in python, the rendering part would change according to the data sent back from python. So that we don’t need to change the coeds to much
3. **Art resources hot update**:
Art-side resources shouldn’t be embedded in the application. All of them are configurable and can be hot updated.  So when it provided as tools, result can be immediately seen without restart the application, after we change the art resources

## Frontend&Backend Architecture
The architecture largely inspired by the modern web stack: HTML/Browser/CSS/JS. Because we have a similar situation.  Instead of a game application, Unity-side, more like a renderer, it renders the information from the python module, and gathers user input sent back to python. It is very similar to the relationship between browser and server. 
![image][unity-arc]


## Frontend Rendering
Same as browser render website by HTML file, we have our own “Markup language” for unity to render. This markup language is much simpler than HTML because it does not try to be general, but only used in this type of game.  
Biggest difference between HTML and ours is that our markup not only has to consider the static things, but also event sequence, animation. Unity also generates the animation based on the game event in markup.

This graphic shows how a markup file in response message is rendered to final elements on the screen. 

![image][unity-render]
## Frontend Animation
### Challenges
In a normal unity game, doing animation is easy since we can get all gameobject instances we want to do animations with. 
But our game is running in python, all the object instances are stored in python runtime. An object instance sharing mechanism is hard to fit into our current request/response architecture between C#/C++
### Solutions
We extend our “markup-language” to support animation. All the markups in one “game sequence markup file”  share the same ID space, so they can find instance by those ID
![image][untiy-animation]
## C#/Python Protocol-based Communication 
Under this architecture, the communication between C# and Python is very clear, C# send request message to Python, Python send response message to C#.

Because request always includes Userinput and response always includes GameSequenceMarkup, we simplified the communication by introducing this architecture!