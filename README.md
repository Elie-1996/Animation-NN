# Animation-NN
Learned Motion Matching, and more...

Here, I will record and track the progress of the project.
__More information about each item can be found under the TODO list in Projects.__

Tracking Progress:

# Week 1-5: 
Was unable to start due to obligations in Computer Vision Research (and HW in week 5)...
* Slight Note: Prior to starting the investigation below, We actually checked out the article on Learned Motion Matching first as well as reading and understanding the paper. The problem was that we couldn't find any implementation online.

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
* Ran various simulations to gain more insight on **system's limits**: \
  -> The "Carry" interaction does not work well when the object the character wants to carry is directly behind it. Occasionally it even fails to complete. \
  -> The character is more responsive when we control it through the keyboard, otherwise the "action" estimation gets confused and its as if the character tries to do multiple actions at once. \
  -> Unsure if I should list this in the limits, but the "idle" state when the character is already sitting causes backward sliding. \
  -> Characters fails to sit correctly on the chair (it misses its arm sometimes).\
  -> If the user "regrets" taking a sit action, then performs a "carry" action, the transition of the animation fails to avoid obstacles, and even it is not smooth.
* Wrote notes on **possible improvements**:\
  -> We can increase the augmented data in the same way, by creating our own scenes. Ideally, it would be to battle cases where we already expected a realistic solution. (For example, trying to carry the object behind the character).\
  -> It would be interesting to let the character adapt to different 3D environment. To achieve this, perhaps we can alter the representation of the scene information to be more complex, for instance, having a neural network output geometry descriptors/feature space. (Although, admittedly this will probably need total retraining of the Neural networks, which takes 1-2 days - There are possible solutions though like azure but they're generally costly and I do not have any experience in Azure). \
  Another step would be to change the geometry encoders. They suggested PointNet++. Perhaps it is worth it to try their direction first. \
  -> I am curious, is the animation working for the character loaded specifically? It would be interesting to see what would happen if we loaded a different skeleton.
* **(In progress)** reading code in Unity and then training, and comparing it to paper...
* Troubleshooting Visual Studio 2019 (unexplained irresponsiveness... and unnecessary hindrance ) - **Fixed after 2 hours**. As a result Unity Projects won't load.
* Troubleshooting Unity. (due to slowness issues of Visual Studio) - **Fixed after another 2 hours**. In case this happens again here is the fix: reload every "Assembly-CSharp" project.

# Week 10:
3-day workload this week. \
* Next, we try to revise and gain additional understanding of the paper in order to understand what is truly going on. Our approach will be to question what each GUI element is telling the user is happening, which will hopefully unveil the general programming ideas beneath the project. \
* Checked out video: https://www.youtube.com/watch?v=7c6oQP1u2eQ&ab_channel=SebastianStarke (Explaining the entrire paper, in a brief manner). \
* **(In Progress)** Let us try to understand the GUI: \
What is "Bidirectional"? \
What is "Environment"? Basically, the way the system detects there is an object. It is a high-level representation of theobject without caring too much about its structure. This is used to avoid obstacles. \
What is "Interaction"? When planning to interact with an object, the system needs to specify the character's end position more accurately. For this, the "Interaction" structure (volumetric representation) of the object is made in order to ensure more precision in the end state. \
What is Current? It denotes continuous action labels changing from zero to one on each of the t (t=13) trajectory points. \
This purely auto-regressive vector can be understood as describing the character state and is composed of seven types of motion, representing idle, walk, run, sit, open, carry and climb. \
What is Goal? It is the goal provided as high-level instruction from the user. It is a vector that says how "sure" we are of the current goal - sit, walk, run, idle, open, carry. (climb is not included, due to accurately being able to time it well). \
That's not all, it produces the future positions and orientations in the 3D world. When using *keyboard* it remains on the 2D-plane of the floor. When interacting with an object -i.e sitting- it encompasses itself onto the origin of that object. \
What is Experts? It is the experts weights. K=10 in the demo, which means we have 10 experts. The jiggly thing is basically telling us how much we trust a specific expert. This is the output of the gating network: the closer the ball is to an expert, the larger the coefficients to its weights which are inputted in "Motion Prediction Network". \
* **(In Progress)** Let us try to understand the paper better: \
What is volumetric representation? Basically cuboids, once we interact with the object its volumentric representation is calculated. Once the character is within close proximity of an object it is detected. \
Highlight: "Zhang et al.[2018] propose a method based on the mixture\
of experts [Jacobs et al. 1991] to construct a real-time character\
controller for quadruped characters."\
Input to the Gating Network? refer to equation (5). \
* Talked to Roi and setup to meet for Thursday.


Thingswe can try to understand the project better: \
1) Try to use less experts. \
2) Try to retrain the networks. \
3) Try to redefine the locations of the "Contacts". \
4) Try to change the environment Radius and height. \


Things we should try: \
1) Terrain: would this project be able to handle movement in terrain? \
* To try this, notice we would need an accurate collider to hit the ground otherwise gravity for objects fails.
* 
2) Skeleton: would this project be able to produce smooth movements on a different skeleton? Perhaps another humanoid, or what about a quadruped character? \
3) Build a scene s.t the room is identical to one we can test in. i.e build an artificial 3D model of an existing room we can test in. \

Questions: \
1) What kind of sensors can we \
** Second day complete for now, will continue tomorrow hopefully will understand the entire GUI.
