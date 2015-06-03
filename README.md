# S-W DropRate Algorithm (SWDA)
## Acknowledgement

> This Algorithm takes this oppotunity to gratefully acknowledge the contributes of Chris Wong, for his outstanding mathematical modelling which resolves the quantification issues.

## What does this algorithm do

This algrithm is aiming to resolve a problem which lasts for a long time : The drop rate, or similar system is too random for a single person in the Games.

Here's the details of this problem:

assume that in a RPG, players are required to loot a special item to unlock the next stage, however, the drop rate is not 100% but less lower likes 50% or 60%. As soon as a NPC is knocked down, a loot will occur, then as a result, for a single player, how many NPCs he must beat to ensure a successful loot?

In mathematics, the result is obvious: unknown.

We all know that due to the feature of random process, no result would be determined before the dice stay. That is, for a single player, it is possible that he has to fight with scores or even hundreds times repeatly. It is a terrible game experience that may cause some severe result.

However, sometimes, the game designers must set the drop rate not one to make the important item cannot be earned easily.

Here is the contradiction, and extremely hard to balance the "Game Difficulty" and "User Experience".

## How does this algorithm do

SWDA is designed to resolve this problem, the basic thinking of coping with it is the "private drop rate" and "statistics drop rate".

As a game designer, it is usually to consider the game-play elements from a view of macroscopical side. That is, what they really need is the statistics results. For instance, 50% drop rate means if there are N players defeat a NPC, approx N/2 of them may get the loot. Or, for a single player, in average, he may earn the loot for approx each two fights.

That is, on the designers' side, the pivotal concept of drop rate is to control the average times of fights. However, from the players' side, an unpredictable result of fight is abhorrent. Players require more immediate and unambiguous award of fights.

To resolve that, SWDA uses an incremental rating which starts from a small number and keep growing until a successful looting happens.

Assume the user A rolls a **N**-sides dice, a "success" means the number is no bigger than **M** (**M** < **N**), for a single roll, the success rate is:

 **M/N**
 
The game starts from M = 1, and for each rolling, if it is **NOT SUCCESS**, M has a self-increment of 1, otherwise, 1 is assigned to M.

It is clear that, at most after N times, the success rate will be N/N which is 1 or 100%, that resolve the first problem : players will win the game in a predictable time.

Then assume that there are a huge number of players roll the N-sides dice together. A new concept is involved here : Turn. For each turn, each player can choose to roll once or not, as soon as all the players make the decision and roll, a turn ends. So, when the **I**th ( **I** >> 1 ) turn ends, what is the **average success rate** of all the players who select to roll?

If we call the number of players who choose to roll is **K**, and **T** of them success, then the **average success rate** is 

 **T/K**

 which is the game designers required.

 With enough samples and turns, the **average success rate** tended to stabilize, and then the second problem is resolved: designers has a reliable average drop rate to evaluate the macroscopical performance of the game.

 
## Special Numbers

During the developing phase, it is important to decide the average rate. That is, the T/K should be set, and then find a proper N for single person. Appreciate to the works from Chris Wong, in spite of the recursive procedure, a distinct N -> T/K curve could be drawn.

Here are several special numbers people may be interested in:

N = 18

starts from 1/18, the average success rate (T/K) is approx 20%

N = 6409

starts from 1/6409, the average success rate (T/K) is approx 1%

and obviously, if N = 1, T/K = 1 also.

