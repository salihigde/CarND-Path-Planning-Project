# The car is able to drive at least 4.32 miles without incident
Car can drive more than 4.32 miles without incident. Key point to succeed this was to use sensor fusion data and find cars nearby. By finding nearby cars on our left, right and front we can decide if we want to change lane or keep the lane.

# The car drives according to speed limit
In code I set car's max speed to 49.5 miles. If car needs to slow because there is car in front in *line 286 in main.cpp* there is condition to increase the speed until it reaches 49.5 miles.

# Max Acceleration and Jerk are not Exceeded.
To prevent max acceleration car speed is increased gradually 0.224 miles per cycle. Jerk in left/right lane changes are prevented by usage of spline library which produces smooth transitions.

# Car does not have collisions.
Car does not have collision because of the logic I added to *line 283 in main.cpp* that makes car slow done if car is closer to front car less than 30 meters.

# The car stays in its lane, except for the time between changing lanes.
Car is able to stay in its lane until it finds safe time to change lane. Logic for changing lane can be found *277-282 lines in main.cpp*

# The car is able to change lanes
The car is able to smoothly change lanes when it makes sense to do so, such as when behind a slower moving car and an adjacent lane is clear of other traffic. Priority for changing can is the left lane. If left lane is not available then car checks the right lane's availability.

# Model Documentation
Step by step model documentation can be found below.

1) Process sensor fusion data to determine cars in front, left and right
2) Find the cars close to our car to decide if we need to switch lane, keep the lane or slow down.
    * If there is car in front of us and left lane is available then switch lane
    * If there is car in front of us and left lane is NOT available but right lane is available then switch lane
    * If there is car in front of us and both left and right lanes are not available then slow down.
    * If road is available increase the speed to max speed.
3) Use previous and future data to move the car properly
    * Create list of previous and future data points
    * Convert these points to local coordinates of the car to simplify the calculation
    * Give these points to spline as an input the generate smooth movements of the car.
    * Convert back the local car coordinates to global coordinates.