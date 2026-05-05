# Practice 5. Model Training and Fine-tuning.

In this exercise you will train an imitation learning policy on the dataset you collected in Practice 4, using the LeRobot framework.

## Prerequisites

- You have a recorded dataset from Practice 4.
- Your environment has a CUDA-capable GPU.
- You are logged in to Weights & Biases (`wandb login`), if you want to follow your training in [wandb.ai/](https://wandb.ai/).

## Model Training

### Overview

You can start training by using the command `lerobot-train`.

You can read the documentation on training [here](https://huggingface.co/docs/lerobot/il_robots#train-a-policy).

The policy you will train is **ACT** (Action Chunking with Transformers), which is well-suited for short-horizon manipulation tasks.

### How to Get Started

Run a short test training first to confirm everything works:

```
lerobot-train \
  --dataset.repo_id=your_path/your_dataset \
  --policy.type=act \
  --output_dir=outputs/train/act_your_dataset \
  --job_name=act_your_dataset \
  --policy.device=cuda \
  --wandb.enable=true \
  --policy.repo_id=your_path/act_your_dataset \
  --steps=100 \
  --log_freq=10
```

A few arguments to pay attention to:

* `steps`: Total number of gradient update steps. Use a small value (e.g. `100`) to test the setup, and a larger value for a real training run.

* `policy.device`: Set to `cuda` to use the GPU. Training on `cpu` is possible but very slow.

* `wandb.enable`: You must be logged in (`wandb login`) before enabling this.

If the trainig does not fit into your GPU, i.e. you get and OutOfMemory error, try to reduce the batch size with the following argument, and try different values:

* `--batch_size=2`

### Training with Checkpointing

For a real training run, add `--save_freq` to periodically save checkpoints:

```
lerobot-train \
  --dataset.repo_id=your_path/your_dataset \
  --policy.type=act \
  --output_dir=outputs/train/act_your_dataset \
  --job_name=act_your_dataset \
  --policy.device=cuda \
  --wandb.enable=true \
  --policy.repo_id=your_path/act_your_dataset \
  --steps=10000 \
  --log_freq=200 \
  --save_freq=1000
```

* `save_freq`: How often (in steps) to save a checkpoint. Checkpoints are saved to `output_dir` and allow you to resume training later.

### Resuming a Training Run

If training is interrupted, you can continue from the last checkpoint:

```
lerobot-train \
  --config_path=outputs/train/act_your_dataset/checkpoints/last/pretrained_model/train_config.json \
  --resume=true \
  --steps=10000 \
  --log_freq=200
```

* `config_path`: Points to the `train_config.json` inside a checkpoint, which restores all settings from that run.
* `resume=true`: Loads the checkpoint weights and continues from where training left off.

## Monitoring Training

If `--wandb.enable=true`, open [wandb.ai](https://wandb.ai) to see live loss curves. The key metric to watch is `train/loss` — it should decrease over time.

## Submission

Please submit Learning Log 5. Let me know whether training ran successfully and what the loss looked like at the end of your run. If you had issues, describe them and we will check together.

If you managed to run the training correctly, and if you used wandb, you can upload a screenshot of the loss curve.
