# Practice 1. Setup and Running MuJoCo.

## Setup the Environment

### Installing on your own computer

0. Install conda. 

1. Create a conda environment:

```
conda create -y -n so101 python=3.12

conda activate so101
```

2. Install ffmpeg into the conda environment

```
conda install ffmpeg=7.1.1 -c conda-forge
```

3. Install lerobot:

```
pip install lerobot==0.5.1
```

4. Install MuJoCo:

```
pip install mujoco==3.6.0
```


### If you use the computers in the Paniikki room:

The necessary setup for at least the first part of the course has been configured. You can load it with:

```
module load courses/CS-E400218
```

Then you can proceed with the exercise.

## Test the MuJoCo installation

To test that mujoco was installed properly, run:

```
python -m mujoco.viewer
```

You should see the empty mujoco editor.


## Download SO101 Model

Next, download the SO101 model information (xmls and mesh files) from https://github.com/TheRobotStudio/SO-ARM100/tree/main/Simulation/SO101. 
You can use: https://download-directory.github.io/

Note that you will need the scene.xml and so101_new_calib.xml files in the same folder location as well as a subfolder named assets with all of the mesh files. I recommend that you place these all of these in a folder of your so101 directory named something like model. The easiest way to do this is to download the entire SO-ARM101 repository as a zip folder and extract the SO101 folder. Your folder paths should look something like this:

```
project_folder/
├── model/
│   ├── scene.xml
│   ├── so101_new_calib.xml
│   └── assets/
│       └── (mesh files)
```


You should navigate to within the project_folder folder in the terminal to run all subsequent code.

```
cd project_folder
```

To test that your model was downloaded correctly, you can open it in a mujoco visualization window using the command:

```
python -m mujoco.viewer --mjcf=model/scene.xml 
```

This opens the model scene.xml which is contains the actual xml (so101_new_calib.xml) as well as some additional items such as a floor and lighting.

If you have downloaded your model correctly, you should see the robot arm in the simulator.


## Submission

In the learning log, please upload a screenshot of the simulation with the SO-101 arm.


## Acknowledgement

The exercise is heavily inspired by the labs in [this course](https://maegantucker.com/ECE4560/assignment4-so101/), and is used with the permission of the course creator. Some parts of the instructions are mostly unchanged from there, others have been adapted.
