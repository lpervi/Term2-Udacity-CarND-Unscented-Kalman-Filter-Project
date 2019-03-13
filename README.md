[image1]: ./outputs/1.png "1"


# The Real Unscented Kalman Filter

This exercise is intended to show the improved robustness of the Real Unscented Kalman filter. This filter is a slight modification of the UKF, requiring no additional computations at all, that makes the filter abosrve second order terms, so improve performances. Proof can be found in [_Perea et al_](https://arc.aiaa.org/doi/10.2514/1.36824)

As a representative example, I've taken an already existing C++ program from the Udacity study program: ["Self-Driving Car Engineer Nanodegree Program"](https://eu.udacity.com/course/self-driving-car-engineer-nanodegree--nd013). This is intended to determine the position of a vehicle based on laser and radar measurements using the UKF, as described in [this tutorial](https://www.cse.sc.edu/~terejanu/files/tutorialUKF.pdf).

My goal is to use this code to show the benefits of the modified UKF. In general, both filters perform similarly, but some ill-conditioned problems may cause the UKF to diverge while the new filter may still provide good performances.


## Problem formulation
For further details on the definition of the state vector, measurements used, noise levels, etc, please check [this]:(https://medium.com/p/155adb7d71a1)


## History of the repository
Udacity proposed this program to their students and provided the main structure of the files [here](https://github.com/udacity/CarND-Unscented-Kalman-Filter-Project). Code gaps were intended to be filled by individual students.
Among the different students that forked and completed the code, I took the one from [MyCodeBits](https://github.com/MyCodeBits/Term2-Udacity-CarND-Unscented-Kalman-Filter-Project/) quite by chance.

There were few minor errors, but after correcting them, the code properly implemented the UKF. You can check the commits, as you please.

Finally, I had to do a great effort to implement the modified UKF. For this, I had to edit the ukf.cpp file and replace this line of code
```
    VectorXd z_diff = z - z_pred;
```
by this
```
    VectorXd z_diff = z - z_sig.col(0);
```

I was exhausted after such work ! :stuck_out_tongue_winking_eye:


## Installation and execution instructions

### Install uWebSocketIO
**MAC / Linux**
This repository includes two files that can be used to set up and install [uWebSocketIO](https://github.com/uWebSockets/uWebSockets) for either Linux or Mac systems. 
1. chmod a+x install-_os_.sh  # os should be your operative system, i.e. mac or ubuntu
2. ./install-_os_.sh 

**Windows**
For windows you can use either Docker, VMware, or even [Windows 10 Bash on Ubuntu](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) to install uWebSocketIO. Please see [this concept in the classroom](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/16cf4a78-4fc7-49e1-8621-3450ca938b77) for the required version and installation scripts.

### Build and execute
Once the install for uWebSocketIO is complete, the main program can be built and run by doing the following from the project top directory.

1. mkdir build
2. cd build
3. cmake ..
4. make
5. ./UnscentedKF


### Generate measurements (in real time)
This project uses the Term 2 Simulator which automatically generates the measurements in real time. It can be downloaded [here.](https://github.com/udacity/self-driving-car-sim/releases)


__Values provided by the Simulator to the C++ program__

["sensor_measurement"] => the measurement that the simulator observed (either lidar or radar)


__Values provided by the C++ program to the Simulator__

["estimate_x"] <= kalman filter estimated position x
["estimate_y"] <= kalman filter estimated position y
["rmse_x"]
["rmse_y"]
["rmse_vx"]
["rmse_vy"]


## Other Important Dependencies

Refer [Udacity link's](https://github.com/udacity/CarND-Unscented-Kalman-Filter-Project) **Other Important Dependencies** section.


## Code Style

[Google's C++ style guide](https://google.github.io/styleguide/cppguide.html) has been used.


![alt text][image1]
