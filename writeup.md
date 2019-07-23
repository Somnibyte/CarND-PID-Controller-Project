## Writeup

### PID Components

### P Component
The P component represnts the proportional factor of `Kp` to the cross track error. Using the component alone (P Controller) helps the vehicle steer in proportion to the cross track error. A high `Kp` value causes the vehicle to steer uncontrollably towards the left and right side of the middle of the road.

![alt text](https://raw.githubusercontent.com/Somnibyte/CarND-PID-Controller-Project/master/high%20kp.gif "high kp")

An extremely low `Kp` value causes the vehicle to adjust it's steering value at a slow rate causing the vehicle to steer off the rooad as the CTE increases.

![alt text](https://raw.githubusercontent.com/Somnibyte/CarND-PID-Controller-Project/master/low%20kp.gif "low kp")

Using a value of `0.2` causes the vehicle to behave appropriately during the beginning of the course, but eventually the vehicle begins to osicillate in the middle of the road. To account for this ossicilation effect I factored in the d component to the total error equation.

### D Component

The d component represents the temporal derivative of the cross track error. Factoring in this component, we can dampen the osicillations caused by solely using the p component. As the `Kd` gain value increases the vehicle begins to oscillate uncontrollably until the vehicle steers off the road. This is due to the vehicle counter steering too much as the CTE changes.

![alt text](https://raw.githubusercontent.com/Somnibyte/CarND-PID-Controller-Project/master/high%20kd.gif "high kd")

A small `Kd` value seems to eleviate this issue.


### I Component

A systematic bias may be present during the lifetime of our vehicle (misalligned wheels, etc..). To account for this we must factor in the `I` component. The I component represents the sum of the cross track errors over time. If I decrease the `Ki` gain value to a substantially low number the vehicle begins to oscillate.

![alt text](https://raw.githubusercontent.com/Somnibyte/CarND-PID-Controller-Project/master/high%20ki.gif "high ki")

The reason that this occurs is because as the CTE increases the `Ki` gain doesn't contribute to the total error value causing the vehicle to not adjust to systematic biases that may be present. The `Ki` value was increased in order to handle systematic biases that may occur.


The final values that were used for the PID controller were as follows:

`Kp` = 0.2
`Kd` = 0.0009
`Ki` = 3

Result:

![alt text](https://raw.githubusercontent.com/Somnibyte/CarND-PID-Controller-Project/master/final.gif "final")

### Process of choosing values
I discovered these values through trial and error using the feedback described in the individual components above.
