# ROS2 6-DOF Robotic Arm Simulation

Software-in-the-loop simulation of a custom 6-axis articulated robotic arm. Goal is to learn kinematics, control, and motion planning fundamentals by taking a SolidWorks CAD model through to a working ROS2/Gazebo simulation.

## Status

Planning stage. CAD not started. This README locks in scope and phase order before mechanical design begins.
Date of start- 14th Sept 2026

## Scope

- Scale: small desktop arm, ~30-40cm reach, learning-scale (not industrial payload)
- Actuators (for physical prototyping later): steppers + gearing
- Gripper: included in CAD/URDF from the start for correct mass and mounting, but not actuated/simulated until the pick-and-place phase

## Tech Stack

| Layer | Tool |
|---|---|
| Mechanical design | SolidWorks |
| CAD -> URDF | sw2robot |
| Middleware | ROS2 |
| Physics simulation | Gazebo |
| Low-level control | ros2_control (JointTrajectoryController) |
| Motion planning | MoveIt2 |

## Phases

### Phase 1 — CAD & URDF
- Model full 6-DOF arm in SolidWorks, gripper included as an assembly (correct joint origins, axes, mass/inertia)
- Export via sw2robot to URDF/xacro
- Separate visual meshes (high-poly) from collision meshes (simplified primitives/convex hulls) for every link

### Phase 2 — TF2 & Kinematics
- Load URDF in RViz2, verify TF tree: every joint's rotation axis and zero position correct
- Hand-calculate forward kinematics for at least one pose, cross-check against RViz
- Gripper stays a static/fixed link here, no actuation

### Phase 3 — ros2_control + Gazebo
- JointTrajectoryController config for the 6 arm joints
- Spawn in Gazebo, confirm joints respond to commanded trajectories
- Gripper joints can be added to controller config but left uncommanded

### Phase 4 — MoveIt2 Motion Planning
- MoveIt Setup Assistant, planning group for the 6 arm joints
- IK solver (KDL to start), collision-free planning to XYZ targets

### Phase 5 — Pick-and-Place (extended)
- Add gripper planning group, program open/close actuation
- Spawn objects in Gazebo, grasp/lift/sort

### Phase 6 — Eye-in-Hand Perception (extended)
- RGB-D sensor on wrist link
- Point cloud generation fed into MoveIt planning scene for dynamic obstacle avoidance

### Phase 7 — Toolpath Execution (extended)
- Continuous end-effector paths (e.g. welding seam, 3D print contour) via Cartesian planning

## Design Notes

- Phases 1-4 are sequential dependencies: CAD must be correct before URDF, URDF/TF before control, control before planning. Phases 5-7 are independent of each other and can be done in any order once Phase 4 works.
- Wrist joint arrangement (spherical wrist vs. other) is being decided separately during arm design, not finalized in this README.