---
title: Geometry Dash
layout: archive
---
Geometry Dash is a video game where you play as a block that jumps to avoid spikes. Because the game is an autoscroller, the only controls is pressing the jump button at the correct intervals. All of the stages are the same every time, so technically, hard coding a jumping sequence at specific time intervals could complete a stage, but it wouldn't allow for the program to complete other stages.


### Inputs

For our AI to be able to actually play the game, we need to give it information about where the spikes are. We don't have internal data on where they are, so the best we can do is use whatever the user gets. In this case, it's the screen.

This situation would best fit a convolutional neural network where we feed the screen and extract the features regarding the spikes to the network. There are many approaches we could take. One is directly feeding the screen and learning a direct binary output on when to jump. This is the most end-to-end approach but could be the most difficult to learn. Alternatively, we can use the screen and perform object identification to first identify spikes. We can then feed the location of the spike as a distance and let the AI determine when to jump based on that distance.

As we try to build this AI, we can see which method works best.

{: style="text-align:center"}
![Geodash](/assets/images/geodash/geodash.PNG) | ![GeodashGrey](/assets/images/geodash/geodash_grey.PNG)

When downsampled to a 128x128 image, the screen for Geometry Dash looks like this.

{: style="text-align:center"}
![GeodashDown](/assets/images/geodash/downsampled.PNG)

## Training
### Genetic Algorithm

The model can be trained in various ways. As titled, the first I'd like to try is using a genetic algorithm. This is an optimization algorithm that explores an optimization space by creating generations of individuals. The performance of each individual is measured, and those that perform the best are used to create the next generation.

### Reinforcement Learning

The alternative approach is using reinforcement learning to create a model. As this is a discretized action space, we could look into deep-Q networks to solve this problem. As this is an onboard problem (we don't have a model to use, we have to learn by actually playing the game itself), a DQN implemented with memory could be very useful. However, we would be saving an entire screen's worth of information at every instance.

### Resetting the game
In order to determine that we've finished an instance of the game, we check to see if the reset button is available. We take a small bounding box where the reset button should be and compare it directly to a saved image of the same "reset" condition. Whenever this condition is met, we stop our training for the instance.


{: style="text-align:center"}
![GameOver](/assets/images/geodash/gameover.PNG)
