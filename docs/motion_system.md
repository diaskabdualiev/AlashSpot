# 🏁 Motion state controller

The motion controller is a finite state machine that allows for static and dynamic posing, 8-phase crawl, bezier-based trot gait, and choreographed animation.

## Controller Input Mapping

The controller input is interpreted differently between the modes. For walking, it looks like this:

| Controller Input | Mapped to Gait Step | Range   |
| ---------------- | ------------------- | ------- |
| Left x joystick  | Step x              | -1 to 1 |
| Left y joystick  | Step z              | -1 to 1 |
| Right x joystick | Step angle          | -1 to 1 |
| Right y joystick | Body pitch angle    | -1 to 1 |
| Height slider    | Body height         | 0 to 1  |
| Speed slider     | Step velocity       | 0 to 1  |
| S1 slider        | Step height         | 0 to 1  |
| Stop button      | E stop command      | 0 or 1  |

<!-- ### Static and dynamic posing -->

## Walking gait

General description of walking gait.

Time step

Phase condition

Stance and swing controller

## 8-phase crawl gait

The 8-phase crawl gait works by lifting one leg at a time while shifting the body weight away from that leg.

As the name implies, the gait consists of 8 discrete phases, which represent which feet should be in contact with the ground or in swing.

At each time step the phase time $t\in [0,1]$ is updated. When $t\geq 1$ the phase index is updated and phase time is reset.

Is derived from [mike4192 spotMicro](https://github.com/mike4192/spotMicro)

## Trot gait (12 point bezier curve)

The trot gait implements a phase time $t\in[0,1]$, but instead of using contact phases we define a swing/stance ratio of phase time offset for each leg.

The stance controller implements a sin curve to control the depth of steps.

The swing controller implements a bezier curve using 12 control points centered around the robot leg.

Rotation is calulated using the same curve
