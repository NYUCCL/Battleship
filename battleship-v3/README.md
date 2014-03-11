# Basic shape search task

The experimental procedure is described in [Gureckis and Markant (2009)](http://gureckislab.org/papers/GureckisMarkantCogSci2009.pdf).


## Data format


The data for each participant is in a single CSV file. The number of games played varied across participants (they were given a fixed time and played at their own pace). 

The first two columns of every row give the subject number and the game number. The third column labels the type of row, with the following possibilies:

"sample"
: A single observation made by the participant. For example:

```    
participant,game,"sample",sample_index,feedback,rt,repeat
```

- ```sample_index```: location of sample within flattened (1x100) gameboard

- ```feedback```: label that was observed

- ```rt```: reaction time in ms

- ```repeat```: if 1, this location had already been uncovered earlier in the game. Note that repeated samples had no effect on the player's score or the display, and can be safely ignored. They are included here for completeness and because RT is measured relative to the previous mouse click (regardless of whether it was a repeated sample or not).

"gameboard"
: The true gameboard for this game, a 1x100 vector of labels (where a label of 0 indicates an empty location, 1 indicates a location belonging to the 1st shape, and so on). The 10x10 grid can be recreated by splitting the vector row-wise (e.g., the first 10 values are the top row of the gameboard).

```
participant,game,"gameboard",0,0,0,1,1,0,0,0...
```

"paintboard"
: The state of the gameboard at the end of the game, following samples and any "painting" decisions made by the participant. Discrepancies between the paintboard and the true gameboard indicate errors (either failing to paint in part of a shape, or painting in a wrong color).

```
participant,game,"paintboard",0,0,2,2,0,0,0,0...
```


## Caveats

- If there is no data for a particular game, that is because the participant did not make any observations and effectively skipped that game.
