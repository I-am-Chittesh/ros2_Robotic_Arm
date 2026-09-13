# ROS2 6-DOF Robotic Arm Simulation

## Overview
A complete software-in-the-loop simulation for a custom 6-Axis Articulated Robotic Arm. This project focuses entirely on locking down the kinematics, control systems, and autonomy stack in ROS2, moving from a raw SolidWorks CAD model to a fully autonomous pick-and-place manipulator in Gazebo.

## Tech Stack
* **Design:** SolidWorks (using `sw2robot` for clean URDF and kinematic generation)
* **Middleware:** ROS2
* **Simulation:** Gazebo 
* **Motion Planning:** MoveIt2
* **Control:** `ros2_control` (JointTrajectoryController)

## Core Capabilities (The Plan)
* **Precision Kinematics:** Full TF2 coordinate tree implementation mapping the exact joint origins and Z-axis rotations of the 6-DOF model.
* **Digital Twin Physics:** Proper separation of high-poly visual meshes and simplified collision geometries (convex hulls/cylinders) to ensure the physics engine runs efficiently.
* **Collision-Free Path Planning:** Utilizing MoveIt2 and Inverse Kinematics (IK) to calculate sweeping trajectories to reach target XYZ coordinates while avoiding dynamic obstacles.

## Extended Features (What We Can & Might Do)
* **Automated Pick-and-Place:** Spawning interactive objects in Gazebo and programming the 2-finger parallel gripper to grasp, lift, and sort them programmatically.
* **Eye-in-Hand Perception:** Mounting a simulated RGB-D sensor to the wrist link to dynamically locate objects in the workspace and generate point clouds for the planning scene.
* **Complex Toolpath Execution:** Feeding continuous vector paths to the end-effector to simulate industrial tasks like following a welding seam or a 3D printing contour.
