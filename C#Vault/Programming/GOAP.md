#AI
## Overview
Goal Oriented Action Planning a.k.a GOAP is a simplified STRIPS-like planning architecture designed to control autonomous charachter behaviors in games. 
We can make our AI reach a certain goal by taking a certain actions without defining a complicated set of rules.

## Concepts
- [[Goals]]
- [[Actions]]
- [[Plan]]

### Basic approach
The simplest algorithm to select the most valuable action to take is a **Greedy Selection algorithm**. 
1. Choose the goal with the highest insistence.
2. Choose the action that lowers that goal the most (best rating).

The main problem of this approach is that it doesn't consider **side effects or time**. It only takes the  'locally' most optimal choice at each step of the algorithm.

### Discontentment 
A solution is to consider every goal and its priority at once.
The **discontentment** is the sum of all the goal's insistence value.
The goal of a character becomes **minimizing discontentment** instead of a single goal's insistence.
Some goals have more influence on the discontentment calculation. (square/cubed or linear weighted function). 
The calculation for each insistence should also take into account the time it takes to perform the action. 
Using a time metric is a bad solution that would lead to a character prefering short actions. 
A better solution would be to include how the goal has changed over time and how much it would take to perform the actions to reach that goal.
*Insistence* = GoalValue + (changeOverTime x ActionTime) 



## World Model
A world model holds important informations about the game's world (direct of based on the character beliefs)

- getActions() -> get a list of all possible actions based on the list of the current situation.
- applyAction(action) -> Applies an action to itself

- copy() -> needed for planning

- calculateDiscontentment()

Action
- time 

Goals
- changeOverTime

The planning algorithm, the world model, actions, goals **are decoupled**.


## Benefits

### Runtime Behaviour benefits
An agent can choose his actions depending on the environment, and dynamically find alternate solutions to problems without relying on a hard-coded response to a specific scenario.
So an agent can handle dependencies that may not have been anticipated at the time of the behavior development.

### Development benefits
Handling every scenarii by hand quicly becomes a mess. 
Having goals with embedded plans means you have to break down goals in order to allow for more possible situations, but the more maintenance/revisiting it will need in case of a design change.
With GOAP, it can be easily handled by adding actions, and preconditions to related actions.
It also ensures a valid plan with the help of the planner, reducing greatly the chance for a human mistake. (ex. invalid embedded action sequence)

### Variety Benefits
GOAP allows for creating a variety of character type that display different behaviors, but also sharing behaviors across projects.
Differents agents can use different subset of actions leading to a variety of behaviors. 
Exemple : a character has *OpenDoor*  and *SmashDoor* actions available, while another only has a *SmashDoor* action. Both actions lead to the same effect.
Using preconditions will allow for choosing between differents actions that have the same result. (e.g the correct mood for choosing between *SmashDoor* and *OpenDoor*)







