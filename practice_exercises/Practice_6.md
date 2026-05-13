# Practice 6. Policy Evaluation.

In this exercise you will evaluate the policy you trained in Practice 5 by running it on the real robot.

## Prerequisites

* You have a trained policy checkpoint from Practice 5.

* The robot and camera are connected and working (same setup as Practice 4).

## Running the Policy on the Robot

### Overview

Evaluation uses the same `lerobot-record` command as data collection, with two main changes: 
* Adding the argument `--policy.path`, which points to your trained checkpoint. The robot will move autonomously based on what the policy predicts — no teleoperation needed.
* Using only the follower arm. Leader arm is not needed for running the evaluation.

The evaluation run also records the episodes, so you can review what the robot did afterward.

### Command

```
lerobot-record \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem5AE60833891 \
    --robot.id=r2_follower_arm \
    --robot.cameras="{ top: {type: opencv, index_or_path: 0, width: 1920, height: 1080, fps: 30}}" \
    --display_data=true \
    --dataset.repo_id=your_name/eval_your_dataset \
    --resume=true \
    --dataset.single_task="Your task description" \
    --dataset.streaming_encoding=true \
    --dataset.encoder_threads=2 \
    --dataset.episode_time_s=10 \
    --dataset.reset_time_s=10 \
    --dataset.num_episodes=1 \
    --dataset.push_to_hub=false \
    --policy.path=outputs/train/act_your_dataset/checkpoints/last/pretrained_model
```

A few arguments to pay attention to:

* `policy.path`: Path to the trained checkpoint. Point this to the `last/` checkpoint or a specific step checkpoint if you want to compare different stages of training.

* `dataset.repo_id`: Use a new repo ID (e.g. prefix with `eval_`) to keep evaluation recordings separate from your training data.

* `dataset.num_episodes`: How many evaluation rollouts to run. Start with a small number (e.g. `1`) and reset the scene to the same starting position between episodes.

* `resume=true`: Allows appending to an existing evaluation dataset if you run evaluation in multiple batches.

## What to Observe

Watch the robot carefully during each episode. Note:

- Does it move in a plausible direction toward the goal?
- Does it complete the task, partially complete it, or fail entirely?
- Are there any unsafe or wrong movements? Be ready to press the emergency stop.

## Submission

Please submit Learning Log 6. Describe how the policy performed — even a rough qualitative assessment is fine (e.g. "it moved toward the object but missed", "it succeeded 2 out of 5 times"). If evaluation did not work, describe the issue and we will check together.

Upload a short video demostrating how the model works on the robot.
