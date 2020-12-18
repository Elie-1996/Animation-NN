# Animation-NN
Learned Motion Matching, and more...

Here, I will record and track the progress of the project.
__More information about each item can be found under the TODO list in Projects.__

Tracking Progress:

# Week 1-5: 
Was unable to start due to obligations in Computer Vision Research (and HW in week 5)...

Starting from week 6, I will try to work at least 2 days every-week to make up for lost time.
# Week 6: 
2-day workload this week. 
* Created a Slack Channel + Invited Roi to Channel.
* Setup a Github + Github Projects TODO list (can be found under Projects). 
* Updated TODOs in Github Projects.
* Setup the Environment: Installed Unity, Visual Studio, C#, PyCharm, Conda, CUDA tools, GeForceExperience, Python, and Pytorch.
* Read the official article and the paper (of Learned Motion Matching) fully. Still need additional understanding.
* Took a brief look at suggested link (https://github.com/sebastianstarke/AI4Animation) AI4Animation. Found out I needed TensorFlow to take a closer look.

# Week 7:
2-day workload this week. (X to be filled later)
* Updated TODOs in Github Projects.
* Setup Tensorflow + Small Ramp up comparing Tensorflow and Pytorch implementation: https://towardsdatascience.com/pytorch-vs-tensorflow-spotting-the-difference-25c75777377b
* Solved issues with Tensorflow Setup + Pytorch that got messed up. (dependency issues - tf didn't compile)
Problem of TF in greater detail (in case of this happening again):
numpy caused all sorts of problems when introduced in a combined environment with TF. To solve this,
start a new environment, and install Numpy 19.4.2 using:

__conda install -c esgf numpy__

Then, install Tensorflow version that comes with the command:

__conda install -c anaconda tensorflow__
* Installed Unity 2018.3.0f2 version - to match AI4Animation installation.
* Successfully ran one of the demos, yay!
* Explored rest of the demos and played with the run-times.
* Very basic and Initial Familiarization with all runs.
* Talked to Roi and got general direction of what to do in the meantime.

# Week 8:
0-day workload this week. (Got ill :()

# Week 9:
2-day workload this week.
* Read the paper and gained general understanding of the code..
* Reported to Roi.
* Ran various simulations to gain more insight on system's limits:
  -> The "Carry" interaction does not work well when the object the character wants to carry is directly behind it. Occasionally it even fails to complete.
  -> The character is more responsive when we control it through the keyboard, otherwise the "action" estimation gets confused and its as if the character tries to do multiple actions at once.
  -> Unsure if I should list this in the limits, but the "idle" state when the character is already sitting causes backward sliding.
  -> Characters fails to sit correctly on the chair (it misses its arm sometimes).
* Wrote notes on possible improvements:
  -> We can increase the augmented data in the same way, but creating our own scenes.
  -> It would be interesting to let the character adapt to different 3D environment. To achieve this, perhaps we can alter the representation of the scene information to be more complex, for instance, having a neural network output geometry descriptors/feature space. (Although, admittedly this will probably need total retraining of the Neural networks, which takes 1-2 days - There are possible solutions though like azure but they're generally costly).
  Another step would be to change the geometry encoders. They suggested PointNet++. Perhaps it is worth it to try their direction first.
  -> I am curious, is the animation working for the character loaded specifically? It would be interesting to see what would happen if we loaded a different skeleton.
* (In progress) reading code in Unity and then training, and comparing it to paper...

