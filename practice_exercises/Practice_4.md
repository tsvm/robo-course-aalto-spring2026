# Practice 4. Data Collection.

In this exercise you will collect data using the LeRobot framework.

You will teleoperate the follower arm using the leader arm, and will record stream from one camera.

## Team Work

For this and the following exercises, as well as for the final project, you can work in a team.

Please make sure that every team member will have the opportunity to learn all steps of the process.

## Goal

The goal for the first iteration is to be able to record a small dataset and make sure everyting works seamlessly. After that you can do a wider scale data collection for a task of your choice.

## Prerequisites

At this point, the framework should be working on your computers, hopefully without problems. 
If this is not the case, please inform the teacher, and you can check the problems together.

## Data Recording

### Overview

You can start recording data by using the command `lerobot-record`.

You can read the documentation of how to record a dataset [here](https://huggingface.co/docs/lerobot/il_robots#record-a-dataset).

Information about the dataset format is available [here](https://huggingface.co/docs/lerobot/lerobot-dataset-v3).


### How to Get Started

You execute the command with for example the following arguments:

```
lerobot-record \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem5AE60833891 \
    --robot.id=r2_follower_arm \
    --robot.cameras="{ top: {type: opencv, index_or_path: 0, width: 1920, height: 1080, fps: 30}}" \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem5AB01575131 \
    --teleop.id=r2_leader_arm \
    --display_data=true \
    --dataset.repo_id=your_name/your_dataset \ # Change the path!
    --dataset.episode_time_s=10 \
    --dataset.reset_time_s=10 \
    --dataset.num_episodes=5 \
    --dataset.single_task="Your task description" \ # Give youw description of the task
    --dataset.streaming_encoding=true \
    --dataset.encoder_threads=2 \
    --dataset.push_to_hub=false \
    --resume=true # <- This is not passed when recording a new dataset.

```

Several aruguments to pay attention to:

* `dataset.repo_id`: If you push to HuggingFace Hub, this will be your username and repository. If saving locally, the dataset will be saved in the CACHE_DIR on your computer, i.e. `$CACHE_DIR/huggingface/lerobot/[the given dataset.repo_id]`.

* `dataset.num_episodes`: The number of episodes, i.e. dmeonstrations that you will record in this run. Start first with a small value, i.e. 5, in order to test how the procedure works.

* `dataset.episode_time_s`: This is the time that one episode will be recorded.

* `dataset.reset_time_s`: This is time to reset the environment to the initial state for the next episode recording.

* `dataset.push_to_hub`: Set to false if you only want to record the dataset on your computer, and not push tothe HF hub.

* `resume=true`: When adding more demonstrations to a dataset, we can resume i.e. append the current run to this dataset, which is specified in the `dataset.repo_id`.

* `robot.cameras`: You can specify one or more cameras. Details below.

### Camera Setup

You need to connect the camera with USB.

Then pass it to the recording command with the following argument:

`--robot.cameras="{ top: {type: opencv, index_or_path: 0, width: 1920, height: 1080, fps: 30}}"`

* **top**: specifies the position/name of the camera. You can use any label here (e.g. `top`, `wrist`, `side`) — it becomes the key used to reference this camera stream throughout the pipeline.

* **type**: the camera backend to use. `opencv` uses OpenCV to interface with the camera, which works with most USB webcams and capture cards on Linux, macOS, and Windows.

* **index_or_path**: identifies which camera to open. An integer (e.g. `0`) selects the camera by device index (as enumerated by the OS), while a string path (e.g. `/dev/video2`) selects it by device path. Use `0` if you only have one camera connected. You can see the connected cameras in Device Manager of your computer.

* **width** / **height**: the capture resolution in pixels. Both the camera and the driver must support the requested resolution — if unsupported, OpenCV will silently fall back to a default. The cameras we have in this course, have values `width: 1920, height: 1080`.

* **fps**: target frame rate. Again, this must be a mode the camera hardware supports. Common values are `15`, `30`, and `60`. `30` should be a good value.


## Examine the Recorded Dataset

Open the directory where the dataset was saved. Examine the files that were recorded. 

## Submission

Please submit Learning Log 4 and describe if you had any problems in the process.

No need to upload any visual proof. Please let me know if you managed to successfully collect data. If not, please explain what kind of issues you are still having and we will check them together.
