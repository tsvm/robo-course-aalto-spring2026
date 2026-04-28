# Practice 1. Pick-and-place in simulation.

In this exercise, you will implement forward kinematics in with the SO-101 arm in the MuJoCo simulator.



## Prerequisites

You should have completed the setup from Practice 1, and should be able to see the SO-101 in the MuJoCo simulation.

The following should work:

```
conda activate so101
python -m mujoco.viewer --mjcf=model/scene.xml 
```

## Implementing pick-and-place in simulation

Download the zip file with the exercise files from MyCourses.

Check the files one by one:
* `so101_mujoco_utils.py`: contains functions for initial pose and moving to a new pose. You don't need to do any modifications in this file. 
* `so101_forward_kinematics.py`: contains functions that create the transformation matrices. 
    * The function `get_forward_kinematics` computer the end-effector pose for a given set of joint angles.
    * The functions `Rx`, `Ry`, `Rz` return the rotations of the x, y, z axes for a given angle.
    * The functions `get_gXY` compute the 4×4 homogeneous transform from joint X to joint Y.
    * In this file, you need to fill the missing displacement and rotations, following the example in the first two functions.
* `pick_and_place_mujoco.py` contains:
    * The function `show_cubes` shows the starting and final positions. They should look like the example on the slides if the forward kinematics was implemented correctly.
    * The starting and final configurations.
    * Calls the function `show_cubes`.
    * In this file, you need to implement the TODOs, which visualize the arm going to start position, closing the gripper, moving to final position, opening the gripper.


When you implement the missing pieces, run the `pick_and_place_mujoco` script:


```
python pick_and_place_mujoco.py
```

And you should see the arm moving from start to final position.


## Submission

When you finish the exercise, please submit Learning log 2, and attach screenshots of the arm on at least the start and final position.


## Acknowledgement
 
This exercise is heavily inspired by the labs in [this course](https://maegantucker.com/ECE4560/assignment6-so101/), and is used with the permission of the course creator. 
