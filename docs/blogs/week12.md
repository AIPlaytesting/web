# Week 12 : Polishing

This week saw refinement of features in our app. We playtested with a CMU faculty for three consecutive days to get a good understanding of how our app feels and if the data it offers is valuable. We got some good suggestions and have kept working on those suggestions to improve the features in the app. The plan going forward is to make sure that our features are polished so that the app can be met with a graceful conclusion in the coming weeks.

## AI Updates

Like last week, there were no algorithmic changes to the reinforcement learning agent. Majority of the work that went in during this week was to create structured data from the training and testing phases of the AI. This is very important to create the visualizations that will be important for designers using the app. Here is a description of some of this data:

### Distributions for Game Length, Game End Player HP, Game End Boss HP:
In the last version of the app, we displayed the average game length, average game end player hp and average game end boss hp. But it was pointed out to us that this data in itself may not be very useful because simply an average does not give a good idea of what is really happening. Taking this into consideration, we now show distributions for each of these variables.

### Anomaly Games
One of the features that was long pending was a view of some of the anomalies (or outliers) detected during the playtesting the game. Some of these anomalies/outliers include:

- The 5 longest games
- The 5 shortest games that were won
- The 5 games with maximum damage in a single turn

Last week, we worked on making sure that these anomalies are tracked and recorded into a json file in a structured way that saves all the game state information for each step of each turn in the game.

### Card Combinations
This was being worked on since the last week. The objective was to show the designer which card combinations were played the most. To this end, we record all combinations of three and four consecutive cards played. For now, the way we visualize this data is to simply show the top 5 three-card combinations. We are still thinking about better ways to visualize this data. A picture of this in action is shown below.

![](/images/week-12-card-combo-seq.png)

## Updates to the Training Section
Training is a very important section because it takes the longest time. Last week, we focused on improving the user experience during training of the app. A picture of how this looks is shown below.

![](/images/week-12-training-1.png)

The new features we added include:

### Parallel Training
- Support for multiple training in parallel.
- Training sessions management.
- Locking training after you have already scheduled a training on a deck (to avoid repetition in training)

### Training Dashboard
- Shows all actively scheduled training in the dashboard with basic information.
- Marks the selected training( for current deck) with different background colors.
- Renders training curve of historical rolling average reward to indicate current training status.
- Fetches data and refresh the training curve every iteration 

## Updates to the Playtest Section

Playtest History

We added a playtest history feature to allow the user to view the completed playtests and compare with different versions. A picture of this is shown below:

![](/images/week-12-playtest-1.png)

The new features include:

- Recording playtest history every time a playtest is finished
- Searching history and filling the history list when the playtest page is refreshed
- Showing basic information (win rate and number of games) on the list
- Loading history and rendering the playtest data when the “View Result” button is clicked

## Distribution Visualization

As pointed out earlier, some of the feedback we got showed us that distributions make more sense than average values in some cases. So this week we added distribution graphs for game length, player/boss HP. The following is an image of the distributions of the player and boss hp:

![](/images/week-12-dist-vis1.png)

The following is some additional information about how this was achieved:

- Used the d3.js API to draw distribution graph
- Calculated the probability density from the given data samples from the playtest
- Automatically adjustes the domain of the axis to make the distribution properly fill the whole graph.
- In the “Ending Margin” section, two distributions were drawn in a single graph.
- Marked different distributions with different colors and names in “Ending Margin” section.

## The Card Relationship Table
Another cool visualization that we have is the card relationship table which shows how many times was a combination of two cards played. This is to give an intuitive sense of card relationships. The following is a picture of how this looks:

![](/images/week-12-card-rel1.png)

The following are some details about this:

- Once again, used d3.js to draw the svg of the relationship table.
- Interpolated the color according to the actual value of each block.
- Highlighted the block when mouse hover
- Added a tooltip to show exact values of that block when mouse hover.
- Displayed the two cards represented by a block on the right side during mouse hover.

## Card Analysis
Although this part already existed last week, we added some improvements to the display of card performance analysis. A picture of this is shown belows.

![](/images/week-12-card-stat1.png)

The following are some additional details about this:

- Drew histograms of card utilization, average play position and play count separately
- Ranked the order in histograms by values
- Drew card images of every card in playtest
- Showed opportunities and card play position as progress bar on the right side of card
- Showed play count as number.

## Card / Deck Editing Updates

### UI Improvements
This week we improved our UI and functionality for editing cards and decks. A picture depicting this is shown below. There are navigation buttons on the left side to go between edit cards or decks. We also added hover events for every card to pop up edit/add icons.

![](/images/week-12-cd-ui.png)

### Add Buffs
This week, we also added a pending feature of adding buffs to cards (in the card edit options). The card edit page can be accessed by clicking on a specific card. We added a “add buff” function for users to include buffs into the card they are editing.

![](/images/week-12-cd-buff.png)

### Confirmation
Lastly, we added confirmation modal functionality from bootstrap into our project. The usage includes delete and save as the picture shown below.

![](/images/week-12-buff.png)

## Playtest Design : Creating Scenarios to Challenge Playtesters
The goal of our project is to make an AI playtest agent that can learn to play a turn based card game and provide valuable feedback to the game designers. This feedback includes:

- Game Balance
    - Economy Balance
- Game Mechanics
    - Game too easy/hard
    - Dominant strategy
- Card Design
- Deck Building

### Building a 100% winrate deck
We wanted to test to see if the AI can achieve a 100% win rate given a very strong deck. The following deck has a ~100% win rate when a human plays it so we know it is very strong.

- Strike+ : Deal 9 damage *4
- Defend : Gain 5 Block *3
- Shrug it off : Gain 8 Block. Draw 1 card.
- Pommel Strike+ : Deal 10 damage. Draw 2 cards
- Flex : Gain 2 strength, and lost it at the end of the game
- Thunderclap : Deal 4 damage and apply 1 vulnerable to all enemies
- Twin Strike+ : Deal 7 damage twice
- Bludgeon : Deal 32 damage

**Reasons why this deck has such a high win rate:**

- Low complexity
    - It only has 8 different cards, 1 debuff for the boss and 1 buff for the player.
    - It only has 13 total cards, each card gets recycled very fast.
- Bludgeon
    - A very useful card that dealt significant amount of damage
- Flex
    - 0 cost card that can boost up attack cards.
    - This card should be played first when drawing it, this will be a good reference for us to see our AI’s strategy.

### What did we learn from this deck?
Actually this is not the first version of the deck. In the very first version, we had [Bludgeon+](https://slay-the-spire.fandom.com/wiki/Bludgeon) and [Bash+](https://slay-the-spire.fandom.com/wiki/Bash) instead of Bludgeon and Thunderclap. And we had a 100% win rate. The reason we decided to change that is because the player could always win by only playing attack cards. If we use the deck to test our AI, it could have a very high win rate even if our AI is not sophisticated enough.

Instead, with the current deck, a random bot will not work. The player needs to manage when to play attack and when to play defend. During the human playtest result, the ending margin of player HP and boss HP are pretty close.

This week saw a lot of polishing to already existing features and addition of a few new features. We hope to continue doing the same for the next week as well.
