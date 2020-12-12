<!-- Copy and paste the converted output. -->

<!-----
NEW: Check the "Suppress top comment" option to remove this info from the output.

Conversion time: 0.851 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β29
* Wed Dec 09 2020 22:39:33 GMT-0800 (PST)
* Source doc: Ziheng's Documentation
----->



# Design

## First Half: Provide scenarios for the development team to make the AI

Our goal is to make an AI playtest agent that could learn to play a turn-based card game and provide valuable feedback to the game designer.

Valuable feedback includes:



*   Game Balance
    *   Economy Balance
*   Game Mechanics
    *   Game too easy/hard
    *   Dominant strategy
*   Card Design
*   Deck Building

To deliver that feedback, the very first thing we need to do is make sure that our AI knows how to play the game, and master the game.


### The first deck that I provided:



*   Strike+ : Deal 9 damage *4
*   Defend : Gain 5 Block *3
*   Shrug it off : Gain 8 Block. Draw 1 card.
*   Pommel Strike+ : Deal 10 damage. Draw 2 cards
*   Flex : Gain 2 strength, and lost it at the end of the game
*   Thunderclap : Deal 4 damage and apply 1 vulnerable to all enemies
*   Twin Strike+ : Deal 7 damage twice
*   Bludgeon : Deal 32 damage

This deck has a 100% win rate when a human player plays it. This means our AI should have a win rate highly close to 100%. This makes it easier for our development team to see how good our AI is. 

This deck is:



*   Easy
    *   It only has 8 different cards, 1 debuff for the boss, and 1 buff for the player.
    *   It only has 13 cards, each card gets recycled very fast.
*   Bludgeon
    *   A very useful card that dealt a significant amount of damage
*   Flex
    *   0 cost card that can boost up attack cards.
    *   This card should be played first when drawing it, this will be a good reference for us to see our AI’s strategy.

We are anticipating our AI will figure out the correct combo of playing Flex Thunderclap and then another attack card.

**What do we learn from this deck?**

Actually, this is not the first version of the deck, in the very first version, we have bludgeon+ and bash+ instead of bludgeon and thunderclap. And we had a 100% win rate. The reason we decided to change that is that the player could always win by only playing attack cards. If we use the deck to test our AI, it could have a very high win rate even if our AI is not sophisticated enough.

After changing to the current deck, a random bot will not work in this situation. The player needs to manage when to play attack and when to play defense. During the human playtest result, the ending margin of player HP and boss HP are pretty close, close to zero.

**How does our AI perform on this deck?**

Our AI finally got nearly 90% of the win rate on this deck, however, it is still not willing to play flex before other attack cards. In the designer’s mind, we thought that always playing flex at the beginning of the turn is an obvious move. The AI is not following that.


### The second deck that I provided:



*   Bash : Deal 8 damage. Apply 2 Vulnerable.
*   Shockwave : Apply 3 Weak and Vulnerable to ALL enemies. Exhaust.
*   Sword Boomerang+ : Deal 3 damage to a random enemy 4 times. *2
*   Cleave+ : Deal 11 damage to ALL enemies. *2
*   Iron Wave : Gain 5 Block. Deal 5 damage. *2
*   Feed+ : Deal 12 damage. If this kills a non-minion enemy, gain 4 permanent Max HP. Exhaust.
*   Clothesline+ : Deal 14 damage. Apply 3 Weak.
*   Heavy Blade+ : Deal 14 damage. Strength affects Heavy Blade 5 times. *2
*   Impervious : Gain 30 Block. Exhaust.
*   Disarm : Enemy loses 2 Strength. Exhaust.
*   Double Tap : This turn, your next Attack is played twice.
*   Uppercut : Deal 13 damage. Apply 1 Weak. Apply 1 Vulnerable.

According to our playtest, we also secured a 100% win rate on this deck. This deck is a lot harder than the first deck, it involves more exhaust cards. Exhaust card means card that only could play once in the entire boss fight.

This deck is:



*   Hard
    *   It has 13 different cards, each of them has unique usability.
    *   It has more buffs.
    *   It only has 2 to 3 defensive cards with less block value.
    *   Majority of the cards cost 2 energy.
*   Double Tap
    *   A powerful card that empowers the next attack cards.
*   Exhaust cards
    *   Can only play once in the entire game. It provides a deeper task to the AI to figure out which turn is the best turn to play the exhaust cards.

**What do we learn from this deck?**

When the AI could win the game, it will not try to maximize its damage in every single turn. So the difficulty of a deck is related to the performance of the AI, if the AI faces a much more difficult deck, it will try to maximize its damage.

	

**How does our AI perform on this deck?**

Our AI finally got 87% of the win rate on this deck, which is pretty good. The AI seems more likely to use 2 same attack cards instead of double tap and then attack card. The results are the same.
