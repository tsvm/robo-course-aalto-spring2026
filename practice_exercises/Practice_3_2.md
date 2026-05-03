# Practice 3. Pick-and-place on the robot.

In this exercise you will implement a simple pick and place movement on the SO-101 follower arm.

## Copying the calibration file

Your calibration file was saved in your computer CACHE folder.

For example, on Mac, the calibration JSON files are saved in `~/.cache/huggingface/lerobot/calibration/`. 

In Windows, check `C:\Users\YourUsername\.cache\huggingface\lerobot\calibration\` (but it might also be another folder, depending on the version of your Windows OS).

Follower arm calibration files are saved in the subfolder `robots/so_follower`, and the leader arm calibration files -- in folder `teleoperators/so_leader`.

For this exercise **you need to copy the follower arm calibration file to your project folder**.

```
# Navigate to your project folder in the terminal
cd $PROJECT_DIR

# create a directory calibration_files

mkdir calibration_files

cp $CACHE_DIR/huggingface/lerobot/calibration/robots/so_follower/robot_id_follower_arm.json calibration_files
```

## Get the exercise starter code

Download the Practice 3 zip file and unarchive it in your project folder.

### Get the file so101_forward_kinematics.py

Copy the file `so101_forward_kinematics.py` from your implementation of Practice 2. 

*If you had problems and could not complete this exercise, ask the teacher to give you this file, if you want to continue.*

### Check the file structure

You should have the following structure:

```
project_folder/
├── calibration_files/
│   ├── robot_id_follower_arm.json <- Use the unique name you gave to your robot
├── config.json
├── joint_configurations.py
├── print_forward_kinematics_for_positions.py
├── pick_and_place.py
├── so101_forward_kinematics.py <- This file came from your implementation of Practice 2.
├── so101_utils.py
```

### Add the correct robot port and name in the config file.

In the file `config.json`, enter the port and ID of the follower arm.


### Explore the code

1. Check the available functions in the file `so101_utils.py`.

2. Check the predefined configurations in the file `joint_configurations.py`

3. The file `so101_forward_kinematics.py` is the same that you had to implement in Practice 2.

4. Execute the file `print_forward_kinematics_for_positions.py` to see the coordinates of the gripper in each given joint configuration.

5. Place an object where you expect the gripper to graps it. You can place just a small object, to verify whether your calculation is correct. You can also mark with a small object the position where you expect the object to be released.


## Implement the pick-and-place 

In the file `pick_and_place.py`, add the missing code that navigates the arm across the different positions to implement pick-and-place functionality.


## Running the pick-and-place code on the robot

Activate the conda environment:

```
conda activate so101
```

Run the code:

```
python pick_and_place.py
```

*Did you mark the expected pick and place locations correctly?*

You can now put an actual object to be grasped.


## Submission

Send Learning log 3, uploading photos of at least the starting and final position of the pick and place.

## Acknowledgement
 
This exercise is heavily inspired by the labs in [this course](https://maegantucker.com/ECE4560/assignment6-so101/), and is used with the permission of the course creator. 
