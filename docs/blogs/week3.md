# Week 3 : The Card Game

The biggest highlight this was the pivot. Instead of designing our own game, we decided to go with the popular card game ‘Slay the Spire’. There were several reasons for doing this. During a recently held Brainstorming Workshop that involved a lot of second year students, we got some feedback that resembled a lot of the same things we had been hearing from our faculty instructors and others who we had described our project to. Since we were implementing the AI and designing the game at the same time, it would have been easy for us to change the game’s design in order to make it more suitable for AI training. This has never been the purpose of our project. We dont want to be changing the game in order to suit the AI. We want the game and its design to drive the AI instead of the other way round. This is because we want to work towards something that can be extended to other games and other settings. And although we are not looking towards developing an AI that can play multiple card games (this is an extremely difficult task), we need to be able to develop AI for a game not designed by us to convince anyone that our work has merit.

## The Card Game – Slay the Spire
The game that we chose is [Slay the Spire](https://www.megacrit.com/). There are several reasons for choosing this game:

- Simple and Well Designed : Slay the Spire is a well designed game that is a lot of fun to play. The buff system is uniform and consistent which makes it a good setting for AI training. There arent a lot of programming exceptions when it comes to programming which makes the implementation easier.
- PvE : The game is not player versus player which makes the gameplay more deterministic. With the game concept we had earlier, we were heading towards adversarial AI agents that compete with each other to win. Instead, here we have the AI agent playing against a scripted boss. This makes the training process less complex because the environment is relatively much less stochastic.
- Data Driven Design : Each card is basically a data structure with specific values for damage, block and buffs. Thus each card can be stored as its own JSON object and it is simple to modify. It also makes it easier for us to add new cards.

That being said, we are not looking to build an AI system for the entire game. **We are only looking at boss fights with a predetermined deck of cards.** As a result, we are only looking to train the AI to play out boss fights. If the AI can learn how to play the boss fight, we can get an understanding of how easy or difficult it is to beat the boss when the damage, block or buff values are altered.

## Game Jam – Implementation
After deciding that we wanted a already popular card game and then choosing ‘Slay the Spire’, it was time to move towards the implementation. We had already worked towards the implementation of the previous game and as a result we didnt like the fact that we were back to square one. To overcome this, we decided to do a game jam (Wednesday to Friday) where all three programmers drop everything else and work together to quickly implement a playable version of Slay the Spire. The following are some of the requirements we came up with for this rapid implementation to direct us:

- Friendly for AI to play, and also can by played by humans using the terminal
- Clear protocol for the deck and cards for future extensibility (ties into the **Data Driven Design** which we wanted to preserve)  
- Flexible and agile. It is a rapidly made prototype, but the code will serve as the foundation for what we do in the future

Calling this our own little game jam was a great idea. We quickly divided up the work and started while staying connected on Discord to answer each other’s questions. After three long days, we had a terminal-playable prototype of the card game on our hands. It consisted of one boss combat ([The Guardian](https://slay-the-spire.fandom.com/wiki/The_Guardian)) and twelve cards for the player to choose from. The cards that we implemented are as follows:

- [Anger](https://slay-the-spire.fandom.com/wiki/Anger)
- [Defend](https://slay-the-spire.fandom.com/wiki/Defend_(Ironclad))
- [Shrug It Off](https://slay-the-spire.fandom.com/wiki/Shrug_It_Off)
- [Pommel Strike](https://slay-the-spire.fandom.com/wiki/Pommel_Strike)
- [Sword Boomerang](https://slay-the-spire.fandom.com/wiki/Sword_Boomerang)
- [Body Slam](https://slay-the-spire.fandom.com/wiki/Body_Slam)
- [Iron Wave](https://slay-the-spire.fandom.com/wiki/Iron_Wave)
- [Heavy Blade](https://slay-the-spire.fandom.com/wiki/Heavy_Blade)
- [Flex](https://slay-the-spire.fandom.com/wiki/Flex)
- [Double Tap](https://slay-the-spire.fandom.com/wiki/Double_Tap)
- [Disarm](https://slay-the-spire.fandom.com/wiki/Disarm)
- [Clothesline](https://slay-the-spire.fandom.com/wiki/Clothesline)

Currently this game is human playable in the terminal. This will change in the future and the game will be playable through a UI. However, for now the play experience is a little more tedious with the player having to choose every card to play one by one. The following is a screenshot of how that looks.

![aa](/images/week3-blog_terminal.png)

Here is a list of different game systems that have been implemented so far:

- GameManager for managing the game flow, providing API for AI and input management
- Deck management, which provides the ability import cards and deck information from JSON files
- Behavior system for entities such as player and enemy
- Implementation of a decision tree for the boss, which has different modes and various tactics.

The next steps include getting back to developing an AI that can play this game. We are simultaneously getting ready for quarters next which will give us a great chance to get feedback about our plan from ETC faculty.

