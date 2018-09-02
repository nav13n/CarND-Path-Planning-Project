### Model Documentation:

The well documented path planning code implemented in main.py mainly consistof three parts:

#### Prediction:

This part of the code tries to reason about the enviornment based on telemetry and sensor fusion data. More specifically, based on the telemetry and sensor data, it tries to determine if there are any other cars that are approaching too close in the same lane. The closeness is deteremined by the threshold gap between the speed of the incoming car and the speed of our car estimated based on the trajectory of previous path points. It also tries to predict if there is a possibility of lane change.

#### Behavior:
Based on the prediction output, this part of the code encodes rules for intended behavior. More specificaly, this part of the code increases the speed, decrease speed, and makes a lane change whenever safely possible. At the

#### Trajectory:
This part of the code generates the actual trajectory based on the speed and lane output from the behavior, car coordinates and previous path points. After a desired lane of the vehicle has been set,We create (x, y) coordinate of waypoints ahead of the vehicle (taking either previous path's end point as a reference point or car's starting point)using the corresponding spaced (s,d) Frenet coordinates. From these waypoints, we use a spline function to generate evenly spaced points for a smooth trajectory towards a desired horizon. The car is expected to visit each of these points every 0.02 secs, so the number of the points are calculated by N = double N = (target_dist/(0.02*ref_vel/2.24)) in order to travel at the desired reference velocity. In the implementation, 6 waypoints were created and a horizon of 30 m was chosen to generate the desired trajectory.

Using the above implementation, the vehicle is able to drive at least 4.32 miles without incidents, including; exceeding the speed limit, exceeding the max acceleration and jerk, collisions, and going out of lane.
