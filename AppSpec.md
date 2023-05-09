# Texas Hold’em Hand Evaluator Specification for ChatGPT Ingestion

## Overview

The Texas Hold’em Hand Evaluator is a React app that is hosted on Vercel.com. It has two primary uses:

1. Find the best hands - The app will compute two different “best hand” scenarios:
    1. Using the community cards that have been specified (3, 4, or 5 cards), compute the best hand possible on the table (the nuts). 
    2. Using the community cards and the user’s hole cards, compute the best possible hand. 
2. Compare odds - The app will compute the following odds:
    3. The odds of any single player having the nuts.
    4. The odds of the user completing a hand of all ranks using their hole cards and the community cards.

## Technology Requirements

User Browser:
* The user will interact with the app via a web browser that supports HTML5 rendering on any operating system.

Page formatting:
* Content formatting is done using CSS.
* The minimum font size to use is 14pt.
* The app detects and supports formatting for mobile and desktop browsers independently.

React back-end:
* Use Javascript.
* Create all of the imports required for React and Vercel, and don’t require specific library versions when “latest” will work.

## Internal Data Structures

### HandRank

An enumeration containing all of the possible hand ranks from HighCard to StraightFlush in ascending order. 

### Card

An object representing a single card. It has two required properties:
* **Value** - A numeric value from 2 - 14. The value corresponds ot the number on the card with the following exceptions:
    * Jack = 11
    * Queen = 12
    * King = 13
    * Ace = 14
* **Suit** - An enumeration representing the card suit (ex. Clubs, Diamonds, Hearts, or Spades).

### Cards

An object containing the collections of cards. The cards are exposed through two properties:
* **Community **- A collection of card objects representing the community cards. It must contain 0, 3, 4, or 5 cards.
* **Hole** - A collection of card objects representing the user’s hole cards. It must contain 0 or 2 cards. 

### Odds

An object containing the computed odds. It has the following properties:
* **Community** - A floating point number representing the odds of the nuts existing in someone’s hand (the other two cards).
* **Hole** - An indexed list of computed odds for reaching each of the possible hand ranks when combined with the community cards.

## Site Endpoint Spec

Endpoint List:
* /
* /Cards
* /Cards/Community
* /Cards/Hole
* /Odds
* /Odds/Community 
* /Odds/Hole

All endpoints support the GET HTTP method. The following endpoints also support the POST method:
* /
* /Cards
* /Cards/Community
* /Cards/Hole


### Endpoint Functionality

Unless otherwise specified, all GET methods return a JSON-formatted string and all POST methods take a JSON-formatted string.

#### /

The app root. This endpoint always returns a page that displays the current community and hole cards, and displays all computed odds. Additionally, it provides a user-friendly way for the user the to modify the community and hole cards. Modifying the community cards and hole cards together is done through a POST to the /Cards endpoint. Modifying the community cards alone is done through a POST to the /Cards/Community endpoint.  Modifying the hole cards alone is done through a POST to the /Cards/Hole endpoint. 

GET - Display the page. 

POST - Replace the contents of the internal Cards object and display the page. 

#### /Cards

Endpoint used for inspecting and modifying the internal Cards object. 

GET - Return the community and hole cards.

POST - Replace the contents of the internal object. 

#### /Cards/Community

Endpoint used for inspecting and modifying the internal Cards.Community object. 

GET - Return the community cards.

POST - Replace the contents of the internal object.

#### /Cards/Hole

Endpoint used for inspecting and modifying the internal Cards.Hole object. 

GET - Return the hole cards.

POST - Replace the contents of the internal object.

#### /Odds

Endpoint used for inspecting the internal Odds object. 

GET - Return the contents of the object. 

#### /Odds/Community 

Endpoint used for inspecting the internal Odds.Community object. 

GET - Return the contents of the object. 

#### /Odds/Hole

Endpoint used for inspecting the internal Odds.Hole object. 

GET - Return the contents of the object. 
