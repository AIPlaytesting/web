# Summary
## How this architecture solved the challenges mentioned in 'Overview'?
We decoupled the gameplay logic to a individual module, so both player GUI, AI, playtesting can use this module with same APIs.  
And we also try to make our gameplay and AI as generized as possible. After doing this, we separate the everything configurable into a persistence layer. By quering and updateing the data in persistence layer, designer can change the game, train AI and get playtest data without writing codes.

## What is the biggest difference compared to traditional game development?
We found the we write gameplay codes is very different.   
When we develop a game in game engine such as Unity, we write all gameplay, graphics, physics , VFX,etc in game enigne.   
However, because our game need to run both with graphic and without graphic. Separate gameplay logics from game engine and put it into another platform and language is challenging. 

## If we want to develop a game with AI to do the playtesting, can we just follow this architecture? 
Situations could be very different on different games, so it is hard to have one solution can applied to anycase.   
However, we think that "six modules" (AI/ Gameplay/ Database/PlayerGUI/ DataVisualization/ DesignerGUI) represent six general problems every game will meet if it want to use AI to playtest.