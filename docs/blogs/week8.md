# Week 8 : An App Awakens

The biggest event this week, of course, was the halves presentation on Monday. It went pretty well and we got some nice feedback from the faculty later. The progress this week was a little slow on the AI. On the other hand, we have started worked towards an all-inclusive app that will combine all the different pieces that we have been working on. The team also had meetings with some game design faculty this week to try and understand what are the things game designers would potentially look for in a tool like the one we are making.

## Halves Feedback
Here are some avenues we can improve on considering the feedback we received:

- We could have been more clear to show how the AI is improving over iterations
- It was tough to get a clear sense of what we can learn from the AI expert
- Comparison to other machine learning techniques can fetch us some comparative data on how the agent is performing
- We need some sort of external validation (perhaps from ML faculty)\
- We need some playtesting with designers

We agree with all of these points. Over the last few weeks, it has become increasingly clear to us that we need to shift out approach to ensure that we appropriately serve game designers. Up until this point, the focus of our product has been on the technical side. This was logical because without a sound technical foundation, we have no product. However, now that we have an AI that learns to perform decently well (~70% winrate) which enables us to start thinking about serving designers.

External validation is a highlight from this feedback. We need external validation from ML faculty as well as from game designers about how easy it is to use our product. Although our winrate has improved significantly, we believe that there is still room for improvement. Going the last mile is going to require effort and a deeper dive into potential machine learning techniques. Validation from ML faculty could help with this. On the other hand, validation from game designers is absolutely crucial because at the end of the day, this tool is being built to serve them.

## AI Updates
This week did not see any big jumps in the AI performance. Although, we have managed to improve winrate by around 10%. Last week, we had achieved a winrate of ~61%. This week, we have improved a little and are achieving a winrate of ~72-73%.

The technique behind this change involved getting rid of the elaborate reward function we had earlier. This reward function was designed in a way that each card had its own individual logic for calculating reward. The reward function for the card Flex for example, would look at all the attack cards played after Flex in a given turn and try to calculate how much extra damage was done because of Flex and then use that to calculate the reward attributed to Flex. The biggest problem with this technique was that it was not scalable since each card with a buff required a custom reward function.

The new technique is to attribute reward values only for winning or losing the game. There is no intermediate reward calculated for each individual turn. In contrast to the previously used technique, this approach is easily scalable. At the same time, it is also a more intuitive and logical approach since a reinforcement learning agent should only be rewarded for achieving the goal. With the introduction of intermediary reward, we introduce bias into the agent depending on what the human programming the agent thinks is the correct approach.

The other important issue for the week was to focus on figuring out why we see constant drops in the reward value in the training graphs. An example of this can be seen below:

![](/images/week8-training-graph.png)

As you can see from this image, there are consistent and periodic drops in the reward values. This graph shows rolling averages of 20 games. This means that the drop is not limited to a single game but a series of games. We see that as the number of iterations increase, the distance between drops is going down. This might be a clue indicating that as the AI’s age might have something to do with the drops. However, it is still a mystery as to why this is happening.

We initially assumed that the natural culprit for the causing the drops would be Q-model switches. However, there is no logical reason to believe that the Q-model switch is in fact causing this. Not to mention, there are a significantly higher number of drops than Q-model switches. For the graph seen above, there have only been 5 Q-model switches whereas the number of drops is 21.

The other natural culprit for this can be the data collector or the data writer. Perhaps there is nothing wrong with the algorithm instead there is something wrong with the collection and interpretation of this data. After all, we know that the winrate is true because we have tested the trained AI agent multiple times and it is clear that it has learned a lot about the game.

Going into the following week, we will still be looking closely at the AI training to figure this out. We theorize that solving this problem may hold the key to further improve our winrate.

## Gameplay Rebuilding
An important focus of this week has also been to include the remaining portion of the Slay the Spire game that we had initially planned. Right now, there are many Ironclad cards and buffs that are not a part of our game. With the AI working well, we are heading over to include this remaining part in the game.

### Motivations
- Extendibility: We want to add more cards, more buffs, more mechanisms into our game to let the AI play. We need to make some changes on the current game code in order to restructure it so that we can add new features easily.
- Generalize our method: We want to allow the user to customize the game not only on the game data level, but also deep into the gameplay logic level. This, however, should still let AI play the game.

### How it works
- Previously: In the older structure, logic of specific cards was embedded in the gameplay logic. This is convenient. But when we try to add new buffs and new card mechanisms, we need to look at the intertwined gameplay modules to figure out how to make these changes. An illustration of this can be found below:

![](/images/week8-previous-game-logic.png)

- Current: Now there are two parts in our gameplay. One is gameplay core, which provides the basic logic and game mainloop. The other one is gameplay extension, which includes the customized gameplay logic.

The gameplay core provides API , and gameplay extensions use these API. During the runtime, it will dynamically load the gameplay extension code.

To add new mechanism(buffs/card effect), we just simply follow the API, and don’t need change the gameplay core or worry about the details how they are implemented. Below is an illustration of how this would work:


## One App for All

We plan to develop one app for everything, including AI Module, Unity frontend, python gameplay, card/deck editing, data visualization, etc. A screenshot of our first prototype is shown below:

![](/images/week8-desktop-app-welcome.png)

### Motivation
- Accessible to designers: After halves, we started to think about how to serve designers. We need a user friendly GUI to let designers use all the tools we provide.
- Organize our tools chain: We have many tools built on different platforms using different techniques. We even plan to build more tools. This is a good chance for us to bring everything together in an organized and set a precedent for what comes next.
### Consideration of Different Approaches

**System Built in Unity:**

- Pros: Our game’s GUI is developed in Unity, and we are familiar with Unity.
- Cons: Unity’s UI system is not designed for a generalized desktop GUI. This would be a big problem when we try to build complex UI such as data visualization.

**Browser Based : HTML, CSS, JavaScript**

- Pros: Easy to use and easy to develop. Web techniques are convenient and have many libraries and frameworks.
- Cons: Browsers usually don’t support manipulating local files and start executables, which is very important for us.

**Electron** (Finally picked this)

We ended up choosing electron because of two main reasons:

- Uses web standards: Developing a desktop app is basically the same as writing a website in electron. It uses html, javascript and css, and we are already familiar with these techniques. 
- Highlevel, lightweight: Because of html and javascript, developing an app is much easier than other techniques such as windows naive API, Qt, etc.


## An Introduction to Electron
Electron is a framework for creating native applications with web technologies like JavaScript, HTML, and CSS. It takes care of the hard parts so we can focus on the core of our application. Here is a link to its website – https://www.electronjs.org/

We want to build cross-platform desktop apps for designers to use. Functions like create and edit cards, deck building, running training scripts, and view replay in unity can be activated from a central control panel created by Electron. Below is a screenshot of what a homescreen containing this would look like:

![](/images/week-8-homescreen.png)

### Using Electron to Edit Cards
This part of the application was implemented this week. The motivation for doing this is to make it easier for designers to modify cards. We do not want them to open json files and edit values there since this may be a little daunting for those who are not familiar with json files. Instead, now the user can edit a card file and save it using our tool.

## Insights from Meetings with Game Design Faculty
This week we met with Jessica Hammer and Dave Culyba to talk about the different things a game designer would be looking for in our tool. Here is some interesting insights that we got:

- What are the things that an AI playtester can give you but a human playtester cannot? Try to incorporate as many of these things in your tool as possible. There are many things that an AI can quantify but a human cannot.
- Focus on outliers. Highlight and save game trajectories where something out of the ordinary happens. Try to figure out how these trajectories came to be.
- How to average reward values of cards change over iterations during training. This might give important information about how the AI is learning.
- There must be a level of certainty about whether the AI results are true and trustworthy. Is the AI learning similar gameplay as compared to a human. Getting in touch with the Slay the Spire team can help us with this.

Along with these insights, we also got a few suggestions of things we should try and do which we are currently looking into:

- Prepare a list of different statistical values/trends that can be generated using AI Playtesting. Do this as a brainstorming session.
- Write out / role play the conversation a designer would have while looking at our tool. What would go through their heads when interacting with this tool? What are the different questions they would be trying to answer with our tool?

Despite this being the week with halves, we managed to get a lot of things done in a variety of areas. The project is looking more and more promising as each week passes. We are excited about what the future holds in store for us!

