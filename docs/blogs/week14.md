# Week 14 : Final Bug Fixes

This week started off with the softs opening on Monday which was received well. We handed out our playable prototype to the faculty but because of the lengthy nature of the entire process of using our app, no one really playtested the application. However, we were able to show a demo of our app to the faculty and that was much appreciated.

The remainder of the week involved locating and fixing bugs since most of the application is now complete. We made a bug list to go through it methodically and fix parts of the applications that were not functioning as expected. This was accompanied with the team coming together and playtesting the entire process again and again in order to ensure that it worked smoothly. The Unity playable demo was the one with some issues that was worked upon and tested heavily through the course of this week.

## List of Bug Fixes
Here is an exhaustive list of all the bugs that were identified and fixed this week:

- Unity app crashed randomly in the electron build.
- Unity app’s ‘Replay’ button did not work as intended.
- Unity app crashed when the deck had less than 5 cards.
- In the electron application, selecting multiple copies of the same card to add to the deck would actually add only one copy
- Issues when multiple Unity instances are launched at the same time
- Both boss and player will  got additional block on being attacked if they started with a greater than zero block value
- Player got additional block when attacking the boss with an active Thorn buff
- Heavy Blade did not get the full multiplier effect from the strength buff

## Additional Small Features Added
Here is a list of some of the pending features that we added this week:

### Anomalies Visualization
We added a long pending section in the data visualization part of our app called ‘Anomalies’. This will now allows you to see the game history of some of the anomalies encountered during playtesting: shortest win, longest win and maximum damage in a single turn. Below is a screenshot of how this looks:

![](/images/week-14-s1-1024x694.png)

### Minor Improvements in User Experience
In order to improve the user experience, there were some features added to the electron app:

- Decks can now be deleted using the delete deck button

![](/images/week-14-s2.png)

- Add Deck shortcut when the deck is locked

![](/images/week-14-s3-1024x354.png)

- Play button is now disabled if you have a current Unity executable running

![](/images/week-14-s4.png)

Apart from these changes, we also began work on the documentation of our work since this is an important part of our grading for the semester. What we set out to achieve was to give a blueprint to others who may want to do something similar using AI Playtesting. Going into our final week, we shall be preparing for the final presentation, the festival and our final documentation.
