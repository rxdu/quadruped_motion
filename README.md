# quadruped_motion

This repository contains the code for the simulation and motion control of quadruped robots.

Initial model and simulation configurations of the legged robots (namely B2/B2W/GO2/H1) are
from [unitree_mujoco](https://github.com/unitreerobotics/unitree_mujoco).

## Input device access

By default, the control application uses keyboard to switch control mode and capture the control input.

You can check which device corresponds to your keyboard by running the following command:

```bash
$ sudo evtest
```

Your keyboard should be one of the "/dev/input/eventX" devices.

If you can only open the device with root permission, you can add your user to the "input" group:

```bash
$ ls -la /dev/input/event*
# confirm the device is in group "input"
$ sudo usermod -a -G input $USER
```

You need to log out and log in again to make the change effective.

## Run the control application