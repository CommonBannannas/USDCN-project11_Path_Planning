# CarND-Path-Planning-Project Reflection

[//]: # (Image References)

[image1]: ./snapshot.png "Navigating"

### The software is able to navigate up to 21.61 miles without incidents.

![alt text][image1]

### Path Planning Prediction
Here the software uses telemetry and sensor fusion data to predict other cars
trajectories and to reason about the environment surrounding the car.
The code evaluates if:
  1) There's a car ahead
  2) There's a car left or right of the lane (for changing lanes)

The code evaluates the lane and the position of the other cars on the road at the
end of the last iteration (planned trajectory) to avoid dangerous situations. A car
is considered near if it is less than 35m apart from the current position.

(lines 247 - 287)

### Path Planning Behavior

Here the software decides what to do with the given information, change lanes
if another car is on the same lane, speed up or down.

The software increases or decreases speed based on a speed_delta, thus giving the
car more time to react to situations like a collision with the car ahead.

(lines 289 - 310)

### Path Planning Trajectory Generation

The software generates a new trajectory based of the current speed, lane,
outputs from the behavior algorithm and previous waypoints.

The last two waypoints of the previous planned trajectory or the car position if there is no previous trajectory are used. Three points at 35, 70 and 95m are set for the spline fitting.

The coordinates (shift and yaw) are transformed  to local car coordinates

The last two trajectory waypoints are copied to the new generated trajectory and
the rest of the waypoints are generated fitting the spline.

The change in the car speed is determined in the behavior algorithm, however the software
also uses it to increase or decrease the speed in every waypoints of the generated trajectory.

(lines 312 - 417)

#### Model Shortcomings:
A PID or MPC controller could be used to follow the Path Planning output path
extracting the desired speed from the path and then feed that into the controller.
Also for future work a MPC controller could change the cost function and use the distance
to a waypoint on the generated path.
