#AI 
## Overview
A goal is any condition that an agent wants to satisfy.
- An agent can have any number of active goals at the same time.
- A goal knows how to calculate its current relevance, and knows when it's has been satisfied by defining the needed conditions.
- Agents have goals on different levels of abstraction (e.g Survive, Kill Enemies...)
-  Goals need to be **formalized** so they can be **measured** in the character's world : 
	- The goal 'Survive' becomes 'Maximize health' + 'Maximize Saturation'.
- A goal has a level of importance for the character (a weight) -> **Insitence** : 
	- The higher the insistence, the more the influence on the character. A character will take actions to try and reduce insistence.

