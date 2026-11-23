# wm-drones

wm-drones is where I am trying out learned world models on a drone. A world
model predicts what a robot will observe next from what it observes now and the
action it takes.

Most of the new work in robot learning is on arms, and little of it has reached
drones. This repo is for finding out which of it is worth having on one. I am
not committing to any one direction right now. I am trying different things, and
the list below is what I am trying. There is no code yet.

A drone has to be stabilized hundreds of times per second, and these models
produce a chunk of actions a few times per second. In every direction below the
model therefore outputs waypoints or velocity commands, and a conventional
controller tracks them. All flights are simulated.

## Directions

**World action model.** NVIDIA's
[GR00T 2](https://research.nvidia.com/labs/gear/gr00t-2) and
[DreamZero](https://arxiv.org/abs/2602.15922) generate the next camera frames
and the next actions together. Fine-tune one on flights to output waypoints with
the frames it expects to see, and compare it with the same model trained without
the frames. The comparison says whether predicting video helps a drone at all.

**World model as a test track.** Train a video world model on flights and score
policies inside it without flying them. Score the same policies in the simulator
and compare the two.

**Planning in a learned feature space.** Predict in the features of a pretrained
video model (e.g., [V-JEPA 2](https://arxiv.org/abs/2506.09985)) and not in
pixels. A planner tries action sequences in the model and flies the best one.

**Agent over a flight skill.** In GR00T 2 a language model calls the policy as a
tool, with a sentence and points marked on the camera image. Do the same for a
drone. The open part is what the fast layer does while the agent's last answer
goes stale.

**Subgoal images.** In [π0.7](https://arxiv.org/abs/2604.15483) a world model
draws an image of the next subgoal for the policy to reach. Have one draw the
view the drone should reach next, and a small policy fly to it.

## Reading

- [GR00T 2](https://research.nvidia.com/labs/gear/gr00t-2), for where
  manipulation is.
- [AirVLA](https://arxiv.org/abs/2603.25038), which fine-tuned π0 on a real
  drone with a gripper. What the model had learned about seeing carried over
  from arms, and what it had learned about moving did not.
- The [World Models intro](https://gtcloudrobotics.com/world-models/intro/) on
  the course site, for the background.
