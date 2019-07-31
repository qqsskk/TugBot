# TugBot
The TugBot mobile robotics development platform was designed around two objectives:
1. Learn how to develop robots in the ROS ecosystem
2. Develop a system to assist in towing small boats up from and down to the waterfront

These two objectives provide the constraints for the design of the system. In particular, the second objective is fleshed out into the following problem specification:
- Distance between house and lake: 500m
- Mass of boats: 50-200kg
- Speed required: walking speed, 0-5 km/h
- Terrain capabilities: Road surfaces, hill between lake and house

# TugBot Design
The TugBot is a 4 wheel drive skid steer platform. Propulsion is achieved by repurposed HoverBoard wheels controlled by ODrive brushless motor drivers. The HoverBoard wheels provide an integrated motor and wheel assembly with position feedback given by a Hall effect encoder. The wheels are easy to mount by clamping the fixed shaft onto the robot’s chassis. The ODrive motor controllers allow for a digital interface to the precise control of brushless motors. A guide for controlling a HoverBoard wheel with an ODrive controller can be found [here](https://github.com/madcowswe/ODrive/blob/master/docs/hoverboard.md).
Unfortunately, the ODrive does not yet have a well supported C++ ROS driver, so a basic driver was developed: [odrive_cpp_ros](link).

# ROS Packages
The skid steer design of the TugBot is similar to the design of Clearpath’s [Husky](link). The Husky is also developed on the ROS platform and provided the perfect starting point to begin the journey of learning ROS, and deploying it on a custom developed platform. Most of the ROS packages below are adapted from packages designed for the Husky.

## tugbot_base
The tugbot_base package is reponsible for the interface from the ROS system to the ODrive motor drivers. The convention for the control of actuators in a ROS based system is to develop a hardware interface that can be used with the [ros_control](http://wiki.ros.org/ros_control) package.

The four wheels are represented by four joints that could be controlled through a variety of interfaces. For the TugBot, velocity controller of the wheels is desired. This is achieved through the implementation of the velocity joint hardware interface. The interface enables the communication of velocity set points the ODrive axes, as well as the communication of current motor positions back to the ros_control system.
