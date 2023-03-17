# Grid Navigation Actor Critic RL Agent

### Environment
The environment setting is that of a 2-dimensional grid (with obstacles and walls). In the simples setting, a grid of some dimension HxW can be instantiated with 0 obstacles. A target is placed in the grid along with the Actor (at random positions), and the goal is to find the target in the grid. Each step is a -1 reward, and hitting a wall/obstacle leads to GAME OVER with a -10 reward. The environment rewards a large positive reward for successfully finding the target piece on the grid.

#### State Definition
The state of the environment is defined by vector of size 32. The actor has 8 sensors (for each direction) and can sense the distance and the type of entity in each direction of these sensors.

These 32 units (in the state vector) are divided in two groups of 16 each.
The first group contains information about the **normalized** distance: 
- The first 8 correspond to the distance to an obstacle/wall in each direction. 
- The next 8 correspond to the distance to the target, again, in each direction.

As the sensor detects only the first entity it can find in each direction, it needs to store whether it found an obstacle/wall or a target in each direction. This is stored in the next group of 16 units:
- The first 8 in this group correspond to whether there is an obstacle/wall in those directions (1/0).
- The next 8 correspond to whether there is a target in those directions (1/0).

### Running the experiments
To run the experiments and train, simply navigate to `Simulation.ipynb` and run all cells. This should generate a bunch of files.
1. Figures in the `figures/` directory for cumulative rewards and loss history of training for both the actor and the critic.
2. A `replay.txt` that contains the replays of some episodes after each training cycle. 

### Viewing the Replays
This project is accompanied by a replay tool in the `ReplayTool/` directory. To run the replay, open `Replay.ipynb` file and run all the cells. A PyGame window should open up with replays of each episode along with episode number. The tool allows you to navigate between different replays.

### Notes
1. Deleting or caching the `replay.txt` file after each run before starting a new one could be helpful in avoiding mishaps with the replay tool. The replay tool works off of episode numbers stored in the replay file, and starting each new run resets the episode numbers. It's advisable to create a new replay file from scratch for each run.
2. The Replay tool is very rudimentary and serves the purpose of visualizing the agent's learning process. It may have a lot of bugs, please bare with it.
3. The environment rewards and other things about the environment can be tweaked in the `Grid.ipynb` file. 