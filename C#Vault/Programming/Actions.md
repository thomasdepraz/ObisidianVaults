#AI 
## Actions
- An action is an single, atomic step within a plan that makes a character do something.
- It knows its *preconditions* and *effects* that provide a mechanism for chaining actions. (when it can run and what it will do)
- The duration of an action can be short or infinetly long.


They can be added in centrally, this concerns the actions that are always available to a character.
But most of them are context based (world actions)- meaning that they become available depending on the environement of a character a if a certain set of conditions are met.
Most of the time it is a combination of these two.
Each actions are rated against each goals of a character and give a rating of how much an action would impact a certain goal. (e.g Shoot action -> fullfills Kill Enemy goal / worsens Conserve Ammo goal)

