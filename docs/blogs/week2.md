# Week 2 : First Version

Our goal for the week was to start building the first version of our card game. The components of our system architecture include the game kernel, the AI agent and visualization of the game states in Unity. The other important aspect is the design of the card game which is really what everything is for.

## Card Game Design

As discussed in the last week’s post, our strategy is to start with a simple card game and progressively introduce more complexity. This week, we came up with the first iteration of our game and here are the rules.

- Each player will have the same health amount and attack damage.
- Only two kinds of cards inside the deck: Heal and Damage.
- First round each player will have 5 cards and will draw 2 cards each round from the second round.
- Players will take turns, and they will use all of their cards in hand.

## Game Kernel

The following is a list of files that we have implemented and what each of them does:

- GameSimulator.py: Allows us to simulate the game multiple times and view results.
- GameplayKernel.py: Kernel class that instantiates a game state object to ‘play’ the card game.
- commonDef.py: Defines game state related classes in order to have a concise interface for Unity and AI agent training.
- AutoPlayerDef.py: A bot that randomly picks one card from its hand to play out in each round.
- constantDef.py: Defines constant values used in our project.

## AI Agent

Since we cannot use a tabular approach for our game (as the state-action space is very large), we need to use a neural network. The input layer to the neural network will pass in state defining variable values. We still working on a comprehensive list of such variables. The output layer will then give us a probability distribution over the action space. Using this, we can sample from an action from it or simply take the action that has the highest probability (we plan to try both).

![](/images/week2-nn.png)

The design is of the **Policy Gradient** RL method. The algorithm that we will begin with is the Advantage Actor Critic. The reason for beginning with policy based methods (over value based methods) is that they perform better in stochastic environments. This applies to our project, because the same actions can result in a different future states based on the moves made by the opponent. During the course of our project, it is likely that we shall try several different approaches to train our AI. We are open to trying value based methods if the Advantage Actor Critic algorithm does not perform well in our setting.

Another important aspect to consider is the number of states that we pass into the input layer during training. Since playing a particular card could lead to victory multiple turns later, the reward received after taking a particular action must include discounted future rewards as well. This means that we follow a N-step reward where N is the number of future steps to consider for the reward.

## Visualization and Input Handling in Unity
There are several parts to the Unity system that we are building alongside with our Python game.

### Networking System

For playtesting reasons, we want to allow people to play this game remotely. To that end, we are building a networked Unity system that can allow people to provide inputs remotely through the client. We are using Photon to do this.

The reasons for using Photon:

- Provides free server usage within a limit.
- Provides easy-to-use API for building room/lobby-based game service.
- Great support and tutorial resources in Unity.

Using Photon, we have built a basic matching system that works for us. It currently includes functionality for:

- Connecting players to the service. Manage the connection and disconnection.
- Logic of ‘Ready’, ‘Start Game’, and player chat.

Below are some screenshots of how this looks currently.

![](/images/week2-photon.png)

### Rules of communication between Python and Unity (C#)
We have discussed the rules of how AI, Unity logic, python gameplayer will communicate (to ensure less work when we connect everything).

- Definition and format of important classes such as gamestate/user input is predefined and stored in a python file (commonDef.py).
- C#/Python communication: 
    - Only C# accesses Python, not the other way around
    - C# can only do the following:
        - Call functions, share data structures, and get the snapshot of object instances in python. 
- C# and Python will share the definition of classes which are commonly referenced by both.
- Const values and settings will be stored in separate files(XML, JSON, etc.) and will be dynamically loaded when required.

### C# Coding Standard

We added a coding style guide of Unity/C# in our Github repository’s readme file, including rules for class layout, nomenclature, declaration and brace style.