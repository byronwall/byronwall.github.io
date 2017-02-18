---
layout: post
category: blog
published: false
title: Notes on Halite.io bot
---
## Some comments on my Halite.io bot

The Halite.io contest was completed last week, and my bot finished 77th.  That's a good showing but also meant there was room for improvement.  This post will comment on what the bot did well, avenues I tried that didn't bear fruit, and final thoughts on where I thought the bot could improve.

### Things that went well

####Early game path finding

The game follows several distinct stages.  The first stage of the game includes making moves without having contacted an enemy yet.  In this stage, the game is essentially single player and deterministic.  In some sense, you could derive a cost function for game play and optimize it perfectly; there is no enemy to ruin your plans.

In this stage, I believed that the most important aspect was to grow territory and production simultaneously.  I was not concerned about overextending myself in this stage.  Given those goals, I set out to dictate moves to the bot as soon as possible.  In order to do this, the bot needs to account for the strength available at a future point given that some of the pieces involve will move at different times.  For pieces that have small production values, there is not a huge difference between accounting for this time dependence vs. not accounting for it.  When the production increases, the extra gain for one time step can be sizeable.

In order to determine how to make the moves, I used the following algorithm:
 * determine the border pieces that are neutral
 * rate those pieces using a hueristic function: `production / (strength + 1)`
 * put those border pieces into a priority queue and process them in turn

For each piece, a graph based approach was followed to determine the possible moves to reach the target piece.  This graph consisted of all the pieces that were owned by me.  To determine moves that were possible, a Dijkstra style algorithm was used:
 * Start at the target piece
 * For each neighbor to that piece, owned by self, determine the strength available to be moved, and add to a priority queue.  The priority queue will hold the sets of pieces that are available to make the moves.  The tuple on the queue also stores all the available neighbors.
 * This new square is added to a path and pushed into the heap.
 * The heap is popped to get the current best path (greatest total strength).
 * Each square available (at the border of the current path) is added to the path in turn and those new paths are pushed onto the heap.  Again, the heap is sorted by total strength of the path.
 * If the new square added to the path is farther away from the target than all others (could be +1 square away), then the strength available is increased by the production of all the squares on the path.  In this way, the increasing strength is accounted for.
 * If the path has enough strength to take the target square, that path is added to a separate priority queue as a possible result.
 * If the path size is larger than the maximum allowed (was typically set to 5), then the path was discarded.
 * For future paths, they will only be added to the results queue if they are shorter or have a greater strength for the same distance.
 * The best set of pieces is returned (along with their distance to the target).
 
Now that a set of pieces has been chosen, the actual moves are determined to get the set of pieces to the target.  The goal is to move the pieces at the last possible move.  To do this, the pieces in the set are iterated.  A move is created in the future based on the maximum distance for the set and the distance of the current piece.  In this way, each piece moves as late as possible, and they combine into a single large piece before the final move.

Once the moves are added for those squares, the squares are flagged as unavailable for travel for subsequent paths.  This prevents one set of moves for a less valuable target from interfering with the best paths.  This also has the affect of drastically limiting the number of available paths for later squares.  This helps to avoid blowing up in terms of the complexity of traversing the graph.

Overall, this approach was very effective at growing the territory quickly.  The real advantage of this approach is that combining pieces is handled from the outset. When a map had low production at the start, the bot does a good job of combining squares.

The downside of this approach was the evaluation of the border pieces.  The value of a border piece was the ratio of produciton to strenght.  There was also a blurring of hte nearby values to help provide some high level guidance.

Another downside of this approach was that once the territory grew to be larger than 5 sqaures wide, it was possible for a square near the border to not be included in a future set.  This meant that those pieces were taken out of the action and their strength simply increased.  Ideally, I would have found a way to push those "dead" pieces forward to help with the growth.  In general this was not typically a deal breaker.  For most maps, the pieces would quit moving around the time an enemy was encountered.  That kicked off the second stage of the bot.

#### Cutover to attack mode

Once an enemy was encountered, the bot switched modes from a single player mode to an attack mode.  When switching over, the main difference was the evaluation of border pieces and the move making algorithn.  In general, the 2nd stage of the game used a less sohpisticated algorithm and simply tried to push forward and take space.

My bot did a good job of typically having a large territory and slight advantage on strength when switching modes.  The goal was then to put that strength into the enemy and try to capture their pieces.

The general algorithm in attack mode consisted of:
 * Determine those squares that are within X (typically 5, 7, or 9) pieces of the border. These were considered the pieces that needed to generally head toward a specific square.
 * For each piece that was close to the edge, it iterated through all of the border pieces (I know, awful idea, very slow) and found the closest piece that was worth attacking.  For equally close pieces, it used a hueristic to evaluate which piece to head for.
 * The bot tracked the expected strength for each sqaure and did not allow a move if the new strength would be greater than 255.  Otherwise, the square was moved toward the target.
 * For squares within the interior (not at the border), they were simply moved outward toward a border.
 
The attack procedure was OK but generally not very targeted.  The bot did a poor job of going after specific enemy pieces or areas.  It also had no overarching direction for where to head or when to take squares.  It simply pushed into the enemy until it had captured all the squares or was done for.

### Other approaches tried

There were a handful of things that were tried but did not end up in the final bot. Those included different approaches for both stages of the game.

#### Genetic algorithm to find the best starting path

One approach to choose the starting path was a genetic algorithm.  The goal was to get a path of squares to take that woudl maximize the future vlaue of the territory held.  This approach worked OK, but it seemed to generally pick a path that did not appear optimal.  I think the steps required to generate teh path did not give the bot enough time to actually optimize the path.  There were only 15 seconds at the start of the game to do the heavy lifting.

#### Agent based model to attack

Another approach that was attmpted late was to use an agent based model in the attack phase.  The idea was to identify the owned border squares that had the best target areas near them.  Each square was then given a move to make.  The enemy strength nearby was tallied and distributed through each neighbor of the given square.  The squares were then procesed with a priority queue to determine which peice to move next.  For pieces that were moved next, they were told to simply follow the piece in front of them.

This approach did a pretty good job of moving squares out to the border and back filling for moves into the enemy.  I never programmed in heuristics for when to expand instead of attack so the bot... never expanded.  Go figure.  This bot ended up doing well on small maps or when it could quickly overcome the enemy.  As soon as expansion allowed for dwarfing early progress, this bot failed quickly.  This version of the bot got around the top 100.

The upside of this approach is that every square was touched only once so it was blazing fast.

