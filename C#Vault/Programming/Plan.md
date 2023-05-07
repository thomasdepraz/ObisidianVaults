#AI 
## Overview
- A plan is a **sequence of [[Actions]]**. 
- An agent generates a plan in real-time by supplying some goal to satisfy to a system called a **planner**.
- The planner searches for a sequence among the available actions, that takes the character to his goal state.
- A plan can be aborted, if a more relevant goal activates, or the current plan becomes invalid. 

![[GOAP_PlanFormulationProcess.png]]

It is simulated by the character to find out the discontentment he would have after executing the actions.
To get the best plan for the character we have to simulate every possible plan and choose the best one. 
We can  generate the action sequences in a **depth first search** manner and keep track of the branching that has the lowest discontentment at the end.