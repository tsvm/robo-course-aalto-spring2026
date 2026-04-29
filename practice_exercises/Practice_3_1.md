# Practice 3.1. Setup of the robots.

In this exercise, you will:
* setup the access to the robot on your computer
* calibrate both leader and follower arms 
* test teleoperation

First, plug in the follower robot arm in the power, then connect it to your computer with the USB-C cable.

## Finding port

Execute the command `lerobot-find-port` in the terminal. When asked, disconnect the USB cable and press enter.
The command will output the port on which this arm is connecting.

Example output for Mac:

```
Finding all available ports for the MotorBus.
['/dev/tty.usbmodem575E0032081', '/dev/tty.usbmodem575E0031751']
Remove the USB cable from your MotorsBus and press Enter when done.

[...Disconnect corresponding leader or follower arm and press Enter...]

The port of this MotorsBus is /dev/tty.usbmodem575E0032081
Reconnect the USB cable.
```

The port is in the format '/dev/tty.usbmodem575E0032081'.

You need to do this for both the leader and follower arms separately, and write down the ports for each one. Remember which port is for which arm.

## Calibration

First, check the calibration video:
https://huggingface.co/docs/lerobot/en/so101#calibration-video


**You have two options:**
1. Copy the calibration files uploaded to MyCourses and use them directly. This is easier if you change the robot you work on, which is likely to happen in the course.
2. Run the calibration as shown below. You will have to do this for each robot you work with.


### Copying the calibration files

You can download the file `calibration.zip` and unarchive it in your CACHE folder, under `huggingface/lerobot`

You should have the following files:

```
$CACHE_DIR
├── huggingface/
    ├── lerobot/
        ├── calibration/
            ├── robots/
                ├── so_follower/
                    ├── r1_follower_arm.json	
                    ├── r2_follower_arm.json
            ├── teleoperators/
                ├── so_leader/
                    ├── r1_leader_arm.json	
                    ├── r2_leader_arm.json
```

### Run calibration

#### Calibrate the follower arm

Connect the follower arm with the USB cable. Execute the following command:

```
lerobot-calibrate \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem58760431551 \ # <- The port of your robot
    --robot.id=robot_id_follower_arm # <- Give the robot a unique name
```

#### Calibrate the leader arm

Disconnect the follower arm and connect the leader arm. Execute the calibration command for the leader arm.

**Note that the command for the leader arm has different arguments.**

```
lerobot-calibrate \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem58760431551 \ # <- The port of your robot
    --teleop.id=robot_id_leader_arm # <- Give the robot a unique name
```

## Test teleoperation

After you have calibrated both arms, you can test teleoperation.

Connect both arms to your computer with the USB cables and execute the teleoperation command.

*Note*: Sometimes, when you run teleoperation, you can encounter random errors, such as error about missing or not correctly configured motor.
If it is not clear where it comes from, sometimes rerunning the command or reconnecting the robot solves the issue.


```
lerobot-teleoperate \
    --robot.type=so101_follower \
    --robot.port=/dev/tty.usbmodem58760431541 \
    --robot.id=my_awesome_follower_arm \
    --teleop.type=so101_leader \
    --teleop.port=/dev/tty.usbmodem58760431551 \
    --teleop.id=my_awesome_leader_arm
```

