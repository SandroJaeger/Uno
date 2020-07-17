# Project1-Uno
SEI-629 Project 1 - HTML, CSS, JS
<br>
<img src="uno-mockup.png">
<br>
# Welcome to UNO!
<br>
<a href="https://sjaugmented.github.io/Project1-Uno/">Play it here.</a>

# User Story.

The game will start automatically upon loading.

The player and the CPU will each begin with 7 cards, and a number card will begin the Play Pile. The player will go first. The player can either click on a card of matching value or color to play it, play an Action Card (Reverse, Skip, Draw 2, Draw 4, Wild), or if no playable cards are available, click on the Draw Pile for a new card and forfeit their turn.

Next the CPU will play, either playing an appropriate card or taking one from the Draw Pile.

Draw 2 (+2) and Draw 4 (+4) cards will automatically add their amount to the victim's hand and advance the turn. Reverse and Skip cards will both skip the victim's turn (since there are only two players, Reverse essentially becomes a Skip). Wild cards may be played at any time.

The immediate goal is to be the first one to have no cards, at which time the opposing player's cards will be totaled and added to their score according to the following rules:

numbered cards 0-9 = face value
<br>
Reverse, Skip, +2 = 20pts
<br>
Wild, Wild +4 = 50pts

The first player to reach 200 loses the game.


## Cards will be deployed as objects.

Number Cards are straight forward:

red8 = { <br>
    value: 8,<br>
    point: 8,<br>
    color: 'red',<br>
    changeTurn: true,<br>
    drawValue: 0<br>
}

Action Cards will be assigned a value for the sake of logic comparisons, in ascending order of danger to the CPU in the event it loses:

greenReverse = {<br>
    value: 10,<br>
    point: 20,<br>
    color: 'green',<br>
    changeTurn: false,<br>
    drawValue: 0<br>
}

orangeSkip = {<br>
    value: 11,<br>
    point: 20,<br>
    color: 'yellow',<br>
    changeTurn: false,<br>
    drawValue: 0<br>
}

blueDraw2 = {<br>
    value: 12,<br>
    point: 20,<br>
    color: 'blue',<br>
    changeTurn: true,<br>
    drawValue: 2<br>
}

wild = {<br>
    value: 13,<br>
    point: 50,<br>
    color: 'any',<br>
    changeTurn: true,<br>
    drawValue: 0<br>
}

wild4 = {<br>
    value: 14,<br>
    point: 50,<br>
    color: 'any',<br>
    changeTurn: true,<br>
    drawValue: 4<br>
}

The gameController will use the changeTurn and drawValue properties to determine whose turn it is and whether or not any cards need to be drawn.

## CPU LOGIC
The CPU will have two arrays it keeps track of two arrays:

cpuHand = []<br>
playableCards = []

Based on the last card played and it's properties, the CPU will loop through it's cpuHand array, and any card that matches either the value or color of the last card played will be pushed into the playableCards array along with any wilds the CPU may be holding.

Since part of the fun and strategy is knowing when to play your Action Cards, the CPU will randomize their strategy each turn, determined by a Math.Random() variable. If the randomizer is above 0.5, the CPU will prioritize playing Action Cards in an effort to keep their losing score low. If the randomizer is below 0.5, the CPU will hold onto their Action Cards for a later turn and instead play Number Cards. There will also be logic to skip the randomizer once the player gets below a certain number of cards, at which point the CPU will only prioritize Action Cards.


## PLAYER EXPERIENCE
Similar to how the computer will keep track of which cards it can play, so will the gameController do for the player. Should the player click an invalid card, a message will pop up telling the player so. 

These messages and the Game Over screen will be the only on screen prompts in an effort to minimize distractions and allow the flow of the game to take front and center.

(In an effort to protect against unintended clicks, there might be an "Are you sure?" message if the player clicks the Draw Pile while holding playable cards.)

The goal is to create an aesthetically pleasing, minimal-yet-satisfying game loop that is relaxing and entertaining and that - hopefully - users will want to play again and again.